<template>
    <div>
        <el-button type="primary" @click="submitForm()">
            Submit trigger form
        </el-button>
        <!-- <pre class="px-4 rounded-md"> <code class="hljs javascript">javascript
router.<span class="hljs-title function_">get</span>(<span class="hljs-string">'/'</span>, <span class="hljs-function">(<span class="hljs-params">req, res</span>) =&gt;</span> {
  res.<span class="hljs-title function_">send</span>(<span class="hljs-string">'Hello world!'</span>);
});

router.<span class="hljs-title function_">post</span>(<span class="hljs-string">'/users'</span>, <span class="hljs-function">(<span class="hljs-params">req, res</span>) =&gt;</span> {
  <span class="hljs-comment">// Create a new user</span>
});
</code> </pre> -->
    </div>
</template>

<script lang="ts" setup>
import axios from "axios";

let data = ref("");

async function submitForm() {
    /* // Send the HTTP POST request to the server
    fetch("https://ask-stream-zvpnsiaqoa-as.a.run.app/", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            Accept: "text/event-stream",
        },
        body: JSON.stringify({
            messages: [
                {
                    role: "user",
                    content: "How to create simple nodejs api?",
                },
            ],
            session:
                Date.now().toString(36) +
                Math.random().toString(36).substr(2, 5),
        }),
    })
        .then((response: any) => {
            // Process the response, which will include real-time updates delivered through the event stream
            const reader = response.body.getReader();
            function read() {
                reader.read().then(({ done, value }: any) => {
                    if (done) {
                        console.log("Stream closed");
                        return;
                    }
                    const text = new TextDecoder("utf-8").decode(value);
                    console.log(text);
                    read();
                });
            }
            read();
        })
        .catch((error) => {
            console.error(error);
        }); */

    /* const reqBody = {
        messages: [
            {
                role: "user",
                content: "How to create simple nodejs api?",
            },
        ],
        session:
            Date.now().toString(36) + Math.random().toString(36).substr(2, 5),
    };
    const headers: any = {
        "Content-Type": "application/json",
        Accept: "text/event-stream",
    };
    axios
        .post(
            "https://ask-stream-zvpnsiaqoa-as.a.run.app/",
            JSON.stringify(reqBody),
            {
                headers: headers,
                responseType: "stream",
            }
        )
        .then((response) => {
            response.data.on("data", (chunk: any) => {
                const text = new TextDecoder("utf-8").decode(chunk);
                console.log(text);
            });
        })
        .catch((error) => {
            console.log(error);
        }); */

    fetch("/api/cht", {
        method: "POST",
        headers: {
            "Content-Type": "application/json",
            Accept: "text/event-stream",
        },
        body: JSON.stringify({
            message: "How to create simple nodejs api?",
        }),
    })
        .then((response: any) => {
            // Process the response, which will include real-time updates delivered through the event stream
            const reader = response.body.getReader();
            function read() {
                reader.read().then(({ done, value }: any) => {
                    if (done) {
                        console.log("Stream closed");
                        return;
                    }
                    const text = new TextDecoder("utf-8").decode(value);
                    try {
                        console.log(text.trim().replace(/data:/g, ""));
                        console.log(
                            JSON.parse(text.trim().replace(/data:/g, ""))
                        );
                    } catch (error) {
                        console.log(error);
                    }
                    read();
                });
            }
            read();
        })
        .catch((error) => {
            console.error(error);
        });
}
</script>