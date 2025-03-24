---
title: 'Calling MCP Servers the Hard Way'
date: 2025-03-25T00:01:00.000-08:00
draft: false
url: /2025/03/calling-mcp-servers-the-hard-way.html
tags: mcp
---

![https://www.flickr.com/photos/govanriverside/7103908345](images/tin-can-phone.jpg)

Lately, all of the cool kids seem to be doing something with the newest protocol on the block, [Model Context Protocol](https://modelcontextprotocol.io/). Being neither cool, nor a kid, has not stopped me from doing the same of course.

I wanted to test out one of my recent experiments adding [MCP support to wasmVision](https://github.com/wasmvision/wasmvision/blob/main/docs/mcp.md) using that venerable tool of the ancient sages known as [curl](https://curl.se/). Surprisingly, I was unable to find a simple guide to performing this task with the Internet's own universal API client. Here are a few notes that I made to hopefully help out others who would like to explore this newly emerging protocol.

## So what is MCP?

Just in case you have not been hearing all about it, my friend [Philippe Charrière](https://bsky.app/profile/k33gorg.bsky.social) has a [great blog post](https://k33g.hashnode.dev/understanding-the-model-context-protocol-mcp) that explains all.

> The MCP is an open protocol that standardizes how applications provide context to large language models (LLMs). It also provides a standardized way to connect AI models with various data sources and tools.

## How to call MCP servers

Most of the examples on the Interwebs assume that the MCP server is being called via a `stdio` interface. Say what? Even when I run everything on my local machines, I still prefer to use network protocols for when I might, actually, want to run the code someplace else.

Luckily, the authors of MCP did think about this, and provide another way to connect using HTTP. Interestingly, they chose [Server Sent Events (SSE)](https://en.wikipedia.org/wiki/Server-sent_events) as the notifications mechanism. I personally think SSE is a much underutilized protocol, so it was cool to see. 

The data format used for MCP calls is [JSON-RPC 2.0](https://en.wikipedia.org/wiki/JSON-RPC). JSON being human readable vs. binary wire protocols does require more bytes to send/receive to be sure. But especially in the early days of an emerging technology, it is a LOT easier to figure out what is going on, while the tools/patterns/practices catch up with what people are trying to do with that new technology.

The process of calling an MCP server over HTTP/SSE is:

- obtain an MCP session token
- initialize the session
- make calls to the MCP server

## Obtain an MCP session token

First open a new terminal session, and run the following command:

```shell
export MCP_SERVER="http://0.0.0.0:5001"
curl "${MCP_SERVER}/sse"
```

Note that the server address `0.0.0.0:5001` depends on the address of the server that you want to call. Change this to match your desired target server.

You should get a result like this:

```shell
event: endpoint
data: http://localhost:5001/messages?sessionId=5fd5bc15-f2f4-4525-9253-92a96e16f669
```

The curl program instead of exiting immediately, will instead keep running. Do not terminate the running curl program! If you do that, then the SSE session will be ended and the `sessionId` token will be invalid. You will need to call the MCP server using this endpoint with the `sessionId` token from the running session.

## Initialize MCP session

Now you can initialize the MCP session in another terminal window. Make sure you replace the value used for `MCP_ENDPOINT` to match the `data` value returned for the MCP session.

Run the following commands in another terminal session/window:

```shell
export MCP_ENDPOINT="http://localhost:5001/messages?sessionId=5fd5bc15-f2f4-4525-9253-92a96e16f669"
curl -X POST "${MCP_ENDPOINT}" -H "Content-Type: application/json" -d '{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "initialize",
  "params": {
    "protocolVersion": "2024-11-05",
    "clientInfo": {
        "name": "wasmvision",
        "version": "0.3.0-dev"
    }
  }
}'
```

You will need to replace the values for `clientInfo` `name` and `version` to match the MCP server you are wanting to use.

You should see a similar result to the following:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "protocolVersion": "2024-11-05",
        "capabilities": {
            "resources": {}
        },
        "serverInfo": {
            "name": "wasmvision",
            "version": "0.3.0-dev"
        }
    }
}
```

That generally means that it worked, and now you can make calls to the MCP server.

Let's take a peek over at that OTHER terminal session that was still running. Remember the one that was used to obtain the `sessionId` token? You should see some new output similar to this:

```shell
event: message
data: {"jsonrpc":"2.0","id":1,"result":{"protocolVersion":"2024-11-05","capabilities":{"resources":{}},"serverInfo":{"name":"wasmvision","version":"0.3.0-dev"}}}
```

This is the event data being sent by the server in response to the `initialize` call. After all, we *are* using the SSE protocol here, and hence should expect to receive this data.

## List MCP tools

[MCP Tools](https://modelcontextprotocol.info/specification/draft/server/tools/) are services that MCP servers expose to let ML models perform actions against an external system.

To obtain a list of tools:

```shell
curl -X POST "${MCP_ENDPOINT}" -H "Content-Type: application/json" -d '{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "tools/list"
}'
```

You should see output similar to this:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "tools": [
            {
                "name": "exampleTool",
                "description": "An example tool for demonstration purposes",
                "parameters": {
                    "param1": {
                        "type": "string",
                        "description": "The first parameter"
                    },
                    "param2": {
                        "type": "string",
                        "description": "The second parameter"
                    }
                }
            }
        ]
    }
}
```

Discovery complete, now let's call the tool to actually do something.

## Calling MCP tools

To call a specific tool on an MCP server, you need to know the tool name and the required parameters. That just so happens to be the information that we obtained in the previous section.

Here is an example of how to call this tool, named imaginatively `exampleTool`:

```shell
curl -X POST "${MCP_ENDPOINT}" -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "tools/call",
    "params": {
        "tool": "exampleTool",
        "arguments": {
            "param1": "value1",
            "param2": "value2"
        }
    }
}'
```

As usual, replace `exampleTool` with the actual tool name, and provide the necessary parameters in the `arguments` object. You should see a response similar to this:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "output": "Tool execution result"
    }
}
```

This indicates that the tool was successfully called and you have received the result. Imagine what tools like `flyDrone` could do. More on that in an upcoming post...

## List MCP resources

[MCP Resources](https://modelcontextprotocol.info/specification/draft/server/resources/) are a way for MCP servers to share data that is generally well structured, and is also mostly consistent. For example, give me the customer information for account number "1234", or retrieve the current image from my webcam.

To obtain a list of resources:

```shell
curl -X POST "${MCP_ENDPOINT}" -H "Content-Type: application/json" -d '{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "resources/list"
}'
```

You should obtain output similar to the following:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "resources": [
            {
                "uri": "images://output",
                "name": "output",
                "description": "Current output image frame",
                "mimeType": "image/jpeg"
            }
        ]
    }
}
```

We found an image resource! We can now read the data for it.

## Reading MCP resources

To read a specific resource from an MCP server, you need to know the resource URI. This information can be obtained from the list of resources as shown in the previous section.

The fact that a "resource" is obtained by using a consistent URI tells you a lot about the difference in when to use a "resource" as opposed to a "tool".

Here is an example of how to read a resource with the URI `images://output`:

```shell
curl -X POST "${MCP_ENDPOINT}" -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "resources/read",
    "params": {
        "uri": "images://output",
        "arguments": {}
    }
}'
```

You should see a response similar to this:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "data": "a-large-amount-of-base64-encoded-image-data-will-be-here"
    }
}
```

The `data` field contains the base64-encoded content of the image resource. You can decode this data to obtain the original image file.

Now you have successfully read a resource from the MCP server. Give yourself a treat.

## List MCP Prompts

[MCP prompts](https://modelcontextprotocol.io/docs/concepts/prompts) are reusable templates that are intended to let MCP servers define standardized interactions.

You can obtain a list of the prompts like this:

```shell
curl -X POST "${MCP_ENDPOINT}" -H "Content-Type: application/json" -d '{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "prompts/list",
}'
```

If that MCP server has any prompts available, they should appear in the results:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "prompts": [
            {
                "name": "analyze-code",
                "description": "Analyze code for potential improvements",
                "arguments": [
                    {
                        "name": "language",
                        "description": "Programming language",
                        "required": true
                    }
                ]
            }
        ]
    }
}
```

Now that we know what prompts templates are available, we can get one to then use to call our ML system.

## Using MCP Prompts

To use a specific prompt on an MCP server, you need to know the prompt name and the required arguments. This information can be obtained from the list of prompts as shown in the previous section.

Here is an example of how to use a prompt named `analyze-code`:

```shell
curl -X POST "${MCP_ENDPOINT}" -H "Content-Type: application/json" -d '{
    "jsonrpc": "2.0",
    "id": 1,
    "method": "prompts/get",
    "params": {
        "prompt": "analyze-code",
        "arguments": {
            "language": "Golang"
        }
    }
}'
```

Replace `analyze-code` with the actual prompt name and provide the necessary arguments in the `arguments` object. You should see a response similar to this:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {
        "description": "Analyze Golang code for potential improvements",
        "messages": [
            {
                "role": "user",
                "content": {
                    "type": "text",
                    "text": "Please analyze the following Golang code for potential improvements:"
                }
            }
        ]
    }
}
```

Now that we know what question to ask, we can use this prompt when calling your actual ML model. Note that the MCP server is only returning a prompt with which you can call the ML model. It does not actually call the ML server with the obtained prompt.

## MCP Ping

The MCP also has an [optional ping call](https://modelcontextprotocol.info/specification/draft/basic/utilities/ping/) that both clients and servers can make, to tell the other side of the connection that they are still alive.

Try pinging the MCP server like this:

```shell
curl -X POST "${MCP_ENDPOINT}" -H "Content-Type: application/json" -d '{
  "jsonrpc": "2.0",
  "id": 1,
  "method": "ping"
}'
```

You should see a similar result to this:

```json
{
    "jsonrpc": "2.0",
    "id": 1,
    "result": {}
}
```

Good news, you are still connected!

## Conclusion

Kudos to the MCP developers who seem to have taken a pretty good approach for establishing an open protocol using existing standards. MCP is under very active development, and as a result is very likely to change and evolve quickly.

Hopefully, these notes will be helpful to some other human (or machine) that wants or needs to test out that their MCP server is working as expected. This kind of exploration, using well established protocols like HTTP and existing tools like curl, is the cornerstone for development of systems that run on the Internet.
