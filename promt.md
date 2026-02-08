{
  "name": "auto_job_ashwin_html_button",
  "nodes": [
    {
      "parameters": {},
      "type": "n8n-nodes-base.manualTrigger",
      "typeVersion": 1,
      "position": [
        -576,
        -128
      ],
      "id": "5495d040-5f1a-4553-84d1-c2ed9a9e782b",
      "name": "When clicking ‘Execute workflow’"
    },
    {
      "parameters": {
        "documentId": {
          "__rl": true,
          "value": "1UqlTJub5fk8itp8EtVdTFUnpvqYEjqNLlLN4rKd9m8g",
          "mode": "list",
          "cachedResultName": "Auto_apply",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1UqlTJub5fk8itp8EtVdTFUnpvqYEjqNLlLN4rKd9m8g/edit?usp=drivesdk"
        },
        "sheetName": {
          "__rl": true,
          "value": "gid=0",
          "mode": "list",
          "cachedResultName": "Sheet1",
          "cachedResultUrl": "https://docs.google.com/spreadsheets/d/1UqlTJub5fk8itp8EtVdTFUnpvqYEjqNLlLN4rKd9m8g/edit#gid=0"
        },
        "options": {}
      },
      "type": "n8n-nodes-base.googleSheets",
      "typeVersion": 4.7,
      "position": [
        -352,
        -128
      ],
      "id": "67e627f9-2ef4-40b3-a1c7-cd291bdf1153",
      "name": "Get row(s) in sheet",
      "credentials": {
        "googleSheetsOAuth2Api": {
          "id": "vlC9u5I3Y4qevbiC",
          "name": "Google Sheets account"
        }
      }
    },
    {
      "parameters": {
        "jsonSchemaExample": "{\n  \"to\": \"hr email\",\n  \"subject\": \"subject\",\n  \"body\": \"body in html\"\n}"
      },
      "type": "@n8n/n8n-nodes-langchain.outputParserStructured",
      "typeVersion": 1.3,
      "position": [
        112,
        112
      ],
      "id": "6b9531ef-b053-459c-96b5-3e320c562af9",
      "name": "Structured Output Parser"
    },
    {
      "parameters": {
        "promptType": "define",
        "text": "=You are an AI assistant responsible for writing professional HR job application emails.\nThe applicant’s name is **Ashwin Suthar**.\n\nUsing the provided inputs, generate a polished and professional **job application email**.\n\n### Input Fields\n\n* **Company Name:** {{ $json['Company Name'] }}\n* **HR Email ID:** {{ $json['HR Email ID'] }}\n* **Job / Position Name:** {{ $json['Job / Position Name'] }}\n* **Job Description:** {{ $json['Job Description'] }}\n* **Resume Link:** https://drive.google.com/file/d/1fcBD8G_BkSmPanIK84oPJKokWSV8hIfn/view?usp=sharing\n\n### Email Guidelines\n\n* Tone must be **formal and professional**\n* Email type: **Job Application**\n* Address the email as **“Dear Hiring Team,”**\n* Clearly mention the **job position** and **company name**\n* **Do NOT** mention or explain any job description details\n* Keep the content **concise, confident, and corporate-friendly**\n* Explicitly include the sentence: **“My resume is attached below.”** (exact wording)\n\n### Resume Button Requirements\n\n* Include a clickable **“View Resume”** button\n* Button color: **dark black**\n* **No border**\n* Text color: **white**\n* Slight padding with professional spacing\n* Clicking the button must open the resume link\n\n### HTML Formatting Requirements\n\n* The entire email body must be written in **HTML**\n* Use proper paragraph spacing and alignment\n* The resume button must be **centered or neatly aligned**\n* **No emojis**\n* **No placeholders** in the final output\n\n### Ending Requirements\n\n* End with a **polite and professional closing**\n\n### Output Requirements\n\n* Provide a **professional email subject line**\n* Provide the **HTML email body only**\n* The email must be **ready to send without any edits**",
        "hasOutputParser": true,
        "needsFallback": true,
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.agent",
      "typeVersion": 3,
      "position": [
        -128,
        -128
      ],
      "id": "721a88d6-a793-44e1-ad54-bfd062025920",
      "name": "AI Agent"
    },
    {
      "parameters": {
        "sendTo": "={{ $json.output.to }}",
        "subject": "={{ $json.output.subject }}",
        "message": "={{ $json.output.body }}",
        "options": {
          "appendAttribution": false
        }
      },
      "type": "n8n-nodes-base.gmail",
      "typeVersion": 2.2,
      "position": [
        224,
        -128
      ],
      "id": "8dfab973-3fa0-45dd-a56a-a7ba1628be39",
      "name": "Send a message",
      "webhookId": "7b2f87e9-7c4a-435c-9357-32f217d8de00",
      "notesInFlow": true,
      "credentials": {
        "gmailOAuth2": {
          "id": "apPcE7OEw92h3BVP",
          "name": "Gmail account 2"
        }
      }
    },
    {
      "parameters": {
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGoogleGemini",
      "typeVersion": 1,
      "position": [
        -304,
        64
      ],
      "id": "b3c9b754-bc92-4364-894d-55420da1191a",
      "name": "Google Gemini Chat Model",
      "credentials": {
        "googlePalmApi": {
          "id": "jd24qlp7eV5HdcjL",
          "name": "Google Gemini(PaLM) Api account 3"
        }
      }
    },
    {
      "parameters": {
        "model": "openai/gpt-oss-120b",
        "options": {}
      },
      "type": "@n8n/n8n-nodes-langchain.lmChatGroq",
      "typeVersion": 1,
      "position": [
        -96,
        176
      ],
      "id": "5c27cf35-7aee-4e84-ba50-63370eb97870",
      "name": "Groq Chat Model1",
      "notesInFlow": true,
      "credentials": {
        "groqApi": {
          "id": "Zxna4zNpm6mRLusa",
          "name": "Groq account"
        }
      }
    }
  ],
  "pinData": {},
  "connections": {
    "When clicking ‘Execute workflow’": {
      "main": [
        [
          {
            "node": "Get row(s) in sheet",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Get row(s) in sheet": {
      "main": [
        [
          {
            "node": "AI Agent",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Structured Output Parser": {
      "ai_outputParser": [
        [
          {
            "node": "AI Agent",
            "type": "ai_outputParser",
            "index": 0
          }
        ]
      ]
    },
    "AI Agent": {
      "main": [
        [
          {
            "node": "Send a message",
            "type": "main",
            "index": 0
          }
        ]
      ]
    },
    "Google Gemini Chat Model": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 0
          }
        ]
      ]
    },
    "Groq Chat Model1": {
      "ai_languageModel": [
        [
          {
            "node": "AI Agent",
            "type": "ai_languageModel",
            "index": 1
          }
        ]
      ]
    }
  },
  "active": false,
  "settings": {
    "executionOrder": "v1"
  },
  "versionId": "1d8ff2d5-56c5-4f51-b963-0110cb8c6405",
  "meta": {
    "templateCredsSetupCompleted": true,
    "instanceId": "06a43a79163213b7ec86156198eee6a4b6df784cb812e8d566c1929f3a201f7a"
  },
  "id": "3KtavxQCQ4LGKsVm",
  "tags": []
}
