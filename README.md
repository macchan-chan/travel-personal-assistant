## Creating a Generative AI  Travel Assistant App with Amazon Bedrock and AWS Amplify

This is an example shows how to build a travel assistant app. The app will provide a personalized experience by suggesting popular attractions, local experiences, and hidden gems for the user's desired destination. We will build this app using AWS mplify and Amazon Bedrock.

![travel-planner-ai](images/amplify_travel_planner.gif)

## Getting Started
### Clone repo

```

git clone https://github.com/aws-samples/travel-personal-assistant.git
cd travel-personal-assistant

```

### Install the packages

```

npm i

```

### Initiate a cloud sandbox environment

```

npx ampx sandbox

```

### Run the App

```

npm run dev

```


## Security

See [CONTRIBUTING](CONTRIBUTING.md#security-issue-notifications) for more information.

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

---

root/
├── .next/                     # Nextjsのビルドファイル
├── amplify/                   # Amplify設定ファイル
│   ├── backend/
│   │   ├── api/              # GraphQL API定義
│   │   ├── auth/             # Cognito認証設定
│   │   └── function/         # Lambda関数
│   └── team-provider-info.json
├── src/
│   ├── app/                  # Next.js 13+ App Router
│   │   ├── layout.tsx
│   │   ├── page.tsx
│   │   ├── chat/
│   │   └── api/
│   ├── components/           # Reactコンポーネント
│   │   ├── ui/              # 共通UIコンポーネント
│   │   └── features/        # 機能別コンポーネント
│   ├── lib/                 # ユーティリティ関数
│   │   ├── bedrock.ts      # Bedrock関連の処理
│   │   └── amplify.ts      # Amplify設定
│   ├── types/              # 型定義
│   └── styles/             # CSSファイル
├── public/                 # 静的ファイル
├── .env.local             # 環境変数
├── next.config.js         # Next.js設定
├── package.json
└── tsconfig.json

主要な設定ファイル：
amplify/cli.json
{
  "features": {
    "graphqltransformer": {
      "addmissingownerfields": true,
      "improvepluralization": true,
      "validatetypenamereservedwords": true,
      "useexperimentalpipelinedtransformer": false,
      "enableiterativegsiupdates": true,
      "secondarykeyasgsi": true,
      "skipoverridemutationinputtypes": true,
      "transformerversion": 2
    }
  }
}

src/lib/amplify.ts
import { Amplify } from 'aws-amplify';
import awsconfig from '../aws-exports';

Amplify.configure({
  ...awsconfig,
  ssr: true
});


src/lib/bedrock.ts
import { BedrockRuntimeClient, InvokeModelCommand } from '@aws-sdk/client-bedrock-runtime';

const bedrockClient = new BedrockRuntimeClient({
  region: process.env.AWS_REGION
});

// Bedrockクライアントの設定と基本的な呼び出し処理