# Google Generative AI AWS Lambda Layer

A ready-to-use AWS Lambda Layer for the Google Generative AI SDK (`@google/genai`) for **Node.js**. This layer allows you to use Google's Gemini API in your AWS Lambda functions without packaging the dependencies yourself.

## 🚀 Quick Start - Use Pre-built Layer

The easiest way to get started is to use one of our pre-built layers:

### Available Regions

| Region    | ARN                                                          |
| --------- | ------------------------------------------------------------ |
| us-east-1 | `arn:aws:lambda:us-east-1:449296410387:layer:google-genai:1` |
| us-east-2 | `arn:aws:lambda:us-east-2:449296410387:layer:google-genai:1` |
| us-west-1 | `arn:aws:lambda:us-west-1:449296410387:layer:google-genai:1` |
| us-west-2 | `arn:aws:lambda:us-west-2:449296410387:layer:google-genai:1` |
| eu-west-1 | `arn:aws:lambda:eu-west-1:449296410387:layer:google-genai:1` |
| eu-west-2 | `arn:aws:lambda:eu-west-2:449296410387:layer:google-genai:1` |

### Using the Layer in Your Lambda Function

#### Via AWS Console

1. Open your Lambda function in the AWS Console
2. Scroll down to the **Layers** section
3. Click **Add a layer**
4. Select **Specify an ARN**
5. Paste the ARN for your region from the table above
6. Click **Add**

#### Via AWS CLI

```bash
aws lambda update-function-configuration \
  --function-name YOUR_FUNCTION_NAME \
  --layers arn:aws:lambda:us-east-1:449296410387:layer:google-genai:1
```


## 📝 Example Usage

Once the layer is attached to your Lambda function, you can use the Google Generative AI SDK:

```javascript
import {GoogleGenAI} from '@google/genai';

// The client gets the API key from the environment variable `GEMINI_API_KEY`.
const ai = new GoogleGenAI({});

export const handler = async (event) => {
  const response = await ai.models.generateContent({
    model: "gemini-2.5-flash",
    contents: "Explain how AI works in a few words",
  });
  console.log(response.text);
  return response;
};

```

## 🛠️ Building Your Own Layer

If you need a different region or want to customize the layer:

### Prerequisites

- Node.js 20.x or 22.x
- npm
- AWS CLI configured with appropriate credentials

### Steps

1. **Clone or download this repository**

```bash
git clone https://github.com/florisalexandrou/google-genai-lambda-layer.git
cd google-genai-lambda-layer
```

2. **Install dependencies**

```bash
cd nodejs
npm install
cd ..
```

3. **Create the layer package**

```bash
zip -r google-genai-layer.zip nodejs
```

4. **Publish to AWS Lambda**

```bash
aws lambda publish-layer-version \
  --layer-name google-genai \
  --description "Google Generative AI SDK" \
  --zip-file fileb://google-genai-layer.zip \
  --compatible-runtimes nodejs20.x nodejs22.x \
  --compatible-architectures x86_64
```

## 📦 What's Included

- [`@google/genai`](https://www.npmjs.com/package/@google/genai) v1.27.0

## 🔧 Compatible Runtimes

- Node.js 20.x
- Node.js 22.x

## 🏗️ Architecture Support

- x86_64

## 📖 Documentation

- [Google Generative AI SDK Documentation](https://ai.google.dev/gemini-api/docs)
- [AWS Lambda Layers Documentation](https://docs.aws.amazon.com/lambda/latest/dg/chapter-layers.html)
- [Get a Google API Key](https://aistudio.google.com/app/api-keys)

## 📄 License

This layer package is provided as-is. The Google Generative AI SDK is subject to its own license terms.

## ⚠️ Disclaimer

This is an unofficial AWS Lambda Layer. It is not affiliated with, endorsed by, or sponsored by Google or AWS.

---

Made with ❤️ for the serverless community

