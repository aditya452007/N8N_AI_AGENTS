{
  "name": "reddit viral posts",
  "nodes": [
    {
      "parameters": {
        "content": "## SUBREDDITS MOST VIRAL TOP 5 POST ACC. TO UPVOETS AND COMMENTS\n",
        "height": 640,
        "width": 1344
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        544,
        464
      ],
      "typeVersion": 1,
      "id": "d20b5c82-d45f-473e-b893-bd61513a4d38",
      "name": "Sticky Note1"
    },
    {
      "parameters": {
        "mode": "combine",
        "combineBy": "combineByPosition",
        "options": {}
      },
      "type": "n8n-nodes-base.merge",
      "typeVersion": 3.2,
      "position": [
        880,
        864
      ],
      "id": "11f2961c-2dc8-49f2-9d72-9e2f79ff76be",
      "name": "Merge"
    },
    {
      "parameters": {
        "jsCode": "// Code node: \"Subreddit list\"\nconst subs = [\n  'PromptEngineering','ChatGPTPromptGenius','aiagents','n8n',\n'DarkPsychology101','DarkPsychologyTactics','SocialEngineering'\n,'psychology'\n];\n\nreturn subs.map(s => ({ json: { sub: s } }));\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        848,
        544
      ],
      "id": "e9f1a8c6-afd1-4bb5-a850-2fc6cd216ae1",
      "name": "SUB_REDDITS_LIST"
    },
    {
      "parameters": {
        "jsCode": "// Code node: \"Pick top 5 posts per subreddit\"\nconst out = [];\n\nfor (const item of items) {\n  const sub = item.json.sub || item.json.subreddit || 'unknown';\n\n  // Find the listing object inside the merged output\n  // The HTTP node usually returns the JSON listing at the top level.\n  let listing = null;\n  if (item.json && item.json.data && Array.isArray(item.json.data.children)) {\n    listing = item.json; // typical case\n  } else if (item.json && item.json.body) {\n    try {\n      const parsed = typeof item.json.body === 'string' ? JSON.parse(item.json.body) : item.json.body;\n      if (parsed && parsed.data && Array.isArray(parsed.data.children)) listing = parsed;\n    } catch(e) {}\n  }\n\n  if (!listing) continue;\n\n  const posts = listing.data.children.map(c => {\n    const p = c.data;\n    return {\n      subreddit: sub,\n      title: p.title || '',\n      link: 'https://www.reddit.com' + (p.permalink || ''),\n      upvotes: p.ups || p.score || 0,\n      comments: p.num_comments || 0,\n      created_utc: p.created_utc || 0,\n      id: p.id,\n    };\n  });\n\n  // Sort by engagement (simple weighted score: upvotes + comments)\n  posts.sort((a,b) => (b.upvotes + b.comments) - (a.upvotes + a.comments));\n\n  // Take top 5\n  for (const p of posts.slice(0,5)) out.push({ json: p });\n}\n\nreturn out;\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1136,
        864
      ],
      "id": "0e21dc12-0439-4099-9378-00b6d26df966",
      "name": "TOP_5_POST"
    },
    {
      "parameters": {
        "jsCode": "// Code node: \"Make Telegram msg (HTML)\"\nconst htmlEscape = s => (s || '').toString()\n  .replace(/&/g, '&amp;')\n  .replace(/</g, '&lt;')\n  .replace(/>/g, '&gt;');\n\nreturn items.map(it => {\n  const j = it.json;\n  const title = htmlEscape(j.title);\n  const link  = htmlEscape(j.link);\n  const msg =\n    `🔥 <b>${title}</b>\\n` +\n    `👍 ${j.upvotes}   💬 ${j.comments}\\n` +\n    `🔗 <a href=\"${link}\">Open on Reddit</a>\\n` +\n    `<i>r/${j.subreddit}</i>`;\n  return { json: { ...j, msg } };\n});\n"
      },
      "type": "n8n-nodes-base.code",
      "typeVersion": 2,
      "position": [
        1392,
        864
      ],
      "id": "93c242d6-9768-4bf3-9f30-61f6f7e6cf00",
      "name": "TELEGRAM_FREINDLY_MSG"
    },
    {
      "parameters": {
        "chatId": "5567562308",
        "text": "=🔥 {{ $json.title }}\n👍 Upvotes: {{ $json.upvotes }}\n💬 Comments: {{ $json.comments }}\n🔗 {{ $json.link }}\n",
        "additionalFields": {
          "appendAttribution": false,
          "disable_web_page_preview": true,
          "parse_mode": "HTML"
        }
      },
      "type": "n8n-nodes-base.telegram",
      "typeVersion": 1.2,
      "position": [
        1664,
        864
      ],
      "id": "18e1c228-7e70-48bb-903b-7d1fc5d15112",
      "name": "Send Reddit VIRAL Post",
      "webhookId": "dd85f687-12e8-4fe9-a03c-6b54dbf0e9b3",
      "credentials": {
        "telegramApi": {
          "id": "D3crJMacp24An9RP",
          "name": "Telegram account"
        }
      }
    },
    {
      "parameters": {
        "url": "={{ 'https://www.reddit.com/r/' + $json.sub + '/top/.json?t=day&limit=50' }}",
        "options": {
          "batching": {
            "batch": {
              "batchSize": 1
            }
          },
          "response": {
            "response": {
              "responseFormat": "json"
            }
          }
        }
      },
      "type": "n8n-nodes-base.httpRequest",
      "typeVersion": 4.2,
      "position": [
        1136,
        544
      ],
      "id": "712671e1-6a84-4e6f-a31a-da9ce960a1ff",
      "name": "HTTP SUB_REDDITS"
    },
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        592,
        544
      ],
      "id": "fcc28943-9342-4608-8609-392e82a25940",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "content": "## choose your platform\n",
        "height": 464,
        "width": 512,
        "color": 3
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        1984,
        608
      ],
      "typeVersion": 1,
      "id": "10c47b3b-348f-4c0f-8201-c9addba77e89",
      "name": "Sticky Note"
    },
    {
      "parameters": {
        "resource": "message",
        "guildId": {
          "__rl": true,
          "mode": "list",
          "value": ""
        },
        "channelId": {
          "__rl": true,
          "mode": "list",
          "value": ""
        },
        "options": {}
      },
      "type": "n8n-nodes-base.discord",
      "typeVersion": 2,
      "position": [
        2064,
        672
      ],
      "id": "be66ba9f-c3dc-4b4d-ace5-bd28692e9807",
      "name": "Send a message",
      "webhookId": "656521d2-2dd5-4f58-bc98-c94c70459bc7",
      "disabled": true
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.1,
      "position": [
        2064,
        880
      ],
      "id": "bd311967-db75-4446-80cd-3908f7c5f0cd",
      "name": "Send a message1",
      "webhookId": "3902c41d-1c89-4379-a1bb-32c936dcfba6",
      "disabled": true
    },
    {
      "parameters": {
        "operation": "send",
        "additionalFields": {}
      },
      "type": "n8n-nodes-base.whatsApp",
      "typeVersion": 1,
      "position": [
        2272,
        880
      ],
      "id": "99235708-39eb-48ab-a0a5-dee89003103e",
      "name": "Send message",
      "webhookId": "ef410073-6b11-46d0-98f6-63cad642e300",
      "credentials": {
        "whatsAppApi": {
          "id": "uxiJWd9owU4Ztcx6",
          "name": "WhatsApp account"
        }
      },
      "disabled": true
    },
    {
      "parameters": {
        "otherOptions": {}
      },
      "type": "n8n-nodes-base.slack",
      "typeVersion": 2.3,
      "position": [
        2288,
        688
      ],
      "id": "ea7032d6-af43-40ec-8a15-2854a1232fc0",
      "name": "Send a message2",
      "webhookId": "43d61dc6-aa66-428a-8055-459667c3cc20",
      "disabled": true
    },
    {
      "parameters": {
        "content": "# 🚀 Reddit Viral Posts to Telegram Bot (n8n Workflow)\n\nThis bot automatically fetches the **top viral posts of the day** from selected subreddits and sends them to a **Telegram chat** in a clean, readable format.\n\n---\n\n## ⚙️ Workflow Overview\n\nThe workflow consists of the following nodes:\n\n1. **Manual Trigger** → Start the workflow manually.\n2. **SUB_REDDITS_LIST (Code Node)** → Contains the list of subreddits to monitor.\n3. **HTTP SUB_REDDITS (HTTP Node)** → Fetches the top posts (`t=day&limit=50`) from Reddit for each subreddit.\n4. **Merge (Merge Node)** → Combines subreddit info with fetched posts.\n5. **TOP_5_POST (Code Node)** → Selects the top 5 posts per subreddit (based on `upvotes + comments`).\n6. **TELEGRAM_FRIENDLY_MSG (Code Node)** → Formats the post into a Telegram-friendly HTML message.\n7. **Send Reddit VIRAL Post (Telegram Node)** → Sends the formatted posts to your Telegram chat.\n\n---\n\n## 🔧 Setup Instructions\n\n### 1. Prerequisites\n- Install [n8n](https://docs.n8n.io/hosting/) (local, Docker, or cloud).\n- Have a **Telegram Bot Token** from [BotFather](https://core.telegram.org/bots#botfather).\n- Know your **Telegram chat ID** (use `@userinfobot` or send a message to your bot and check logs).\n\n---\n\n### 2. Import the Workflow\n1. Copy the JSON workflow file.\n2. In your **n8n editor**, click:\n   - **Import from File/Clipboard** → Paste JSON.\n3. Save the workflow.\n\n---\n\n### 3. Configure Telegram\n- Open the **Send Reddit VIRAL Post** node.\n- Add **Telegram API credentials**:\n  - **API Token** → From BotFather.\n  - **Chat ID** → Your target Telegram group/user chat ID.\n\n---\n\n### 4. Edit Subreddit List\nInside the **SUB_REDDITS_LIST** code node:\n\n```js\nconst subs = [\n  'PromptEngineering',\n  'ChatGPTPromptGenius',\n  'aiagents',\n  'n8n',\n  'DarkPsychology101',\n  'DarkPsychologyTactics',\n  'SocialEngineering',\n  'psychology'\n];\nreturn subs.map(s => ({ json: { sub: s } }));\n",
        "height": 1424,
        "width": 1056,
        "color": 5
      },
      "type": "n8n-nodes-base.stickyNote",
      "position": [
        -592,
        128
      ],
      "typeVersion": 1,
      "id": "e53cbcda-1655-480d-9a8a-06a03f74d519",
      "name": "Sticky Note2"
    }
  ],
  "pinData": {},
  "connections": {
    "Merge": {
      "main": [
        [
          {
            "node": "TOP_5_POST",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "SUB_REDDITS_LIST": {
      "main": [
        [
          {
            "node": "HTTP SUB_REDDITS",
            "type": "main",
            "index": 0
          },
          {
            "node": "Merge",
            "type": "main",
            "index": 1
          }
        ]
      ]
    },
    "TOP_5_POST": {
      "main": [
        [
          {
            "node": "TELEGRAM_FREINDLY_MSG",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "TELEGRAM_FREINDLY_MSG": {
      "main": [
        [
          {
            "node": "Send Reddit VIRAL Post",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "HTTP SUB_REDDITS": {
      "main": [
        [
          {
            "node": "Merge",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "SUB_REDDITS_LIST",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Send a message": {
      "main": [
        []
      ]
    },
    "Send a message1": {
      "main": [
        []
      ]
    },
    "Send message": {
      "main": [
        []
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "63ba7a91-f4d6-47f4-bd61-fe6ecbd2ce55",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "8998e8f989e529f5a3976189ff512786312515783b3dc1e643e5493181b3f2f2"
  },
  "id": "XWUCiCzyZ5oovUqM",
  "tags": []
}
