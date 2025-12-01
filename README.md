A utility actor that runs a list of actors with a retry mechanism. Avoids memory limit exceeded errors on Apify due to running too many runs in parallel.

<p align="center">
  <img src="https://apify-image-uploads-prod.s3.us-east-1.amazonaws.com/DevbkY3adMTBuoECt-actor-9doUWrGx8wuXIw7Jy-E8KeqgRmE1-Group_54.png" alt="Apify Run Queue" style="height: 60px; margin-right: 15px;" /><a href="https://apify.com/lexis-solutions/apify-run-queue" target="_blank">
    <img src="https://img.shields.io/badge/Try%20it%20on-Apify-0066FF?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNDA4IiBoZWlnaHQ9IjQwOCIgdmlld0JveD0iMCAwIDQwOCA0MDgiIGZpbGw9Im5vbmUiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyI+CjxnIGNsaXAtcGF0aD0idXJsKCNjbGlwMF8zNDFfNDE1NykiPgo8cGF0aCBkPSJNMjE4LjY5NSAxMDRIMzAwLjk3QzMwMi42NDMgMTA0IDMwNCAxMDUuMzU3IDMwNCAxMDcuMDNWMjMyLjc2NkMzMDQgMjM1Ljc3OCAzMDAuMDgzIDIzNi45NDUgMjk4LjQzNCAyMzQuNDI1TDIxNi4xNTkgMTA4LjY5QzIxNC44NDEgMTA2LjY3NCAyMTYuMjg3IDEwNCAyMTguNjk1IDEwNFoiIGZpbGw9IndoaXRlIi8+CjxwYXRoIGQ9Ik0xODkuMzA1IDEwNEgxMDcuMDNDMTA1LjM1NyAxMDQgMTA0IDEwNS4zNTcgMTA0IDEwNy4wM1YyMzIuNzY2QzEwNCAyMzUuNzc4IDEwNy45MTcgMjM2Ljk0NSAxMDkuNTY2IDIzNC40MjVMMTkxLjg0IDEwOC42OUMxOTMuMTU5IDEwNi42NzQgMTkxLjcxMyAxMDQgMTg5LjMwNSAxMDRaIiBmaWxsPSJ3aGl0ZSIvPgo8cGF0aCBkPSJNMjAyLjU5MSAyMDQuNjY4TDEwOS4xMjcgMjk4LjgzNUMxMDcuMjI5IDMwMC43NDcgMTA4LjU4MyAzMDQgMTExLjI3OCAzMDRIMjk2LjhDMjk5LjQ4MyAzMDQgMzAwLjg0MiAzMDAuNzcgMjk4Ljk2NyAyOTguODUyTDIwNi45MDggMjA0LjY4NUMyMDUuNzI2IDIwMy40NzUgMjAzLjc4MiAyMDMuNDY4IDIwMi41OTEgMjA0LjY2OFoiIGZpbGw9IndoaXRlIi8+CjwvZz4KPGRlZnM+CjxjbGlwUGF0aCBpZD0iY2xpcDBfMzQxXzQxNTciPgo8cmVjdCB3aWR0aD0iMjAwIiBoZWlnaHQ9IjIwMCIgZmlsbD0id2hpdGUiIHRyYW5zZm9ybT0idHJhbnNsYXRlKDEwNCAxMDQpIi8+CjwvY2xpcFBhdGg+CjwvZGVmcz4KPC9zdmc+Cg==&logoColor=white" alt="Try it on Apify" style="border-radius: 12px; height: 60px;" />
  </a>
</p>


![Royston queue](https://blogger.googleusercontent.com/img/b/R29vZ2xl/AVvXsEjGFpvvAtASTOq9c2tKHHU_4gTV_Sq_lU0fKxweXu2SvHQR1Tq-Io78aa1zqQntoLaUGwXAV-MDjC7IQya6hYmAHfpa_MOD74yXn9i1z2WeRnNO00PMJSbxnJ5IrWxeO3Vqce4C7w/s1600/royston_queue.jpg)

## Problem Statement 🤔

## 📊 Actor Stats

| Stat | Value |
|------|-------|
| **Version** | `0.0.10` |
| **Last Update** | Dec 1, 2025 |

---



You have a large number of runs you want to start on Apify. However, sometimes your memory limit is exceeded and Apify will not let you start any more runs, and you end up with a lot of failed runs.


## 💻 Integration Examples

This repository includes example code showing how to integrate the `apify-run-queue` actor into your projects.

You can find example implementations in the [`examples/`](./examples) folder:
- **TypeScript/JavaScript**: See [`examples/typescript/`](./examples/typescript) for a complete TypeScript example
- **Python**: See [`examples/python/`](./examples/python) for a complete Python example

Each example includes:
- Ready-to-use code templates
- Setup instructions
- Documentation links

---


## Solution 💡

You can use this actor to run your list of actors in parallel, and it will retry the actors that fail due to memory limit exceeded errors.

## How it works 🤖

- The actor will start running the actors one by one (ℹ️ but won't wait for them to finish). If an actor fails due to a memory limit exceeded error, the actor will wait for some time (default = 30 seconds) and retry.

- The actor will keep track of the number of retries and the total number of runs.

- The actor will run until all actors have started successfully, or failed due to a non-memory limit error (bad input, etc).

## Disclaimer ⚠️

1. This actor will not return results from the actors. Use `webhooks` to get the results from the actors.

2. This actor will run until all actors have started successfully or failed due to a non-memory limit error. This means the run time can be very long. To avoid disruptions, set the actor timeout (under Actor > Settings) to a reasonable value. You can keep the memory limit low, as the actor is just doing scheduling and not processing any data.

## Input 📥

The input is a JSON array of actor calls. Each actor call is an object with the following properties:

- `invocationId`: (optional) Your custom ID for the invocation. You can use this to match input and output.
- `actorId`: The ID of the actor to run.
- `input`: The input to pass to the actor.
- `retryDelaySecs`: The delay in seconds between retries.
- `timeoutSecs`: The timeout in seconds for the actor call.
- `maxItems`: The maximum number of items to process.
- `memory`: The memory in MB to allocate for the actor call.
- `build`: The build to use for the actor call.
- `webhooks`: The webhooks to use for the actor call.
- `isTask`: Whether the actor call is a task. If true, the actorId must be the ID of a task.

## Output 📤

The output is a JSON array of actor calls. Each actor call is an object with the following properties:

- `actorId`: The ID of the actor/task to run.
- `success`: Whether the actor call was successful.
- `runId`: The ID of the run.
- `retries`: The number of retries.
- `error`: The error message. If the actor call was successful, the error is `null`.

## Example Input 📝

```json
{
  "actorCalls": [
    {
      "actorId": "apify/website-content-crawler",
      "invocationId": "my-custom-id",
      "input": {
        "startUrls": [
          {
            "url": "https://www.apify.com",
            "label": "apify.com"
          }
        ]
      },
      "retryDelaySecs": 30,
      "timeoutSecs": 300,
      "maxItems": 100,
      "memory": 2048,
      "webhooks": [
        {
          "eventTypes": ["ACTOR.RUN.SUCCEEDED", "ACTOR.RUN.FAILED"],
          "requestUrl": "https://example.com/webhook"
        }
      ]
    }
  ]
}
```

## Example Output 📤

```json
[
  {
    "invocationId": "my-custom-id",
    "actorId": "apify/website-content-crawler",
    "success": true,
    "runId": "run_123",
    "retries": 0,
    "error": null
  }
]
```

## FAQ

### Doesn't Apify have a built-in retry mechanism?

Not yet. This actor is a workaround to avoid memory limit exceeded errors on Apify.

### Can I use this actor for free?

Yes, you can use this actor for free. However, you will be charged for your usage on Apify.

### How do I know how many runs I can start in parallel?

Your account is limited by how many GBs of RAM you have in your plan. Each actor consumes a set amount of RAM (configurable). You can calculate how many runs you can start in parallel by dividing your RAM by the RAM consumption of the actors you want to run.

---

Got feedback or need an extension?

Lexis Solutions is a [certified Apify Expert](https://apify.com/partners/find). We can help you with custom solutions or data extraction projects.

Contact us on our website [www.lexis.solutions](https://lexis.solutions/contact-us) or [LinkedIn](https://www.linkedin.com/company/lexis-solutions). Happy to help!
