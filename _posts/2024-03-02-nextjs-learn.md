---
title: NextJS Tutorial Learn First
author: happywerrior
date: 2024-03-02 18:35:00 +0900
categories: [Blogging, Nextjs]
tags: [DEV]
---

#### 시스템 요구사항
---

```text
- Node.js 18.17.0 이상
- 운영체제: macOS, Windows(WSL 포함) 또는 Linux
- GitHub 계정과 Vercel 계정도 필요
```
<br />

#### Create a New Project
---
1. Project 폴더 생성
2. Terminal을 열어 생성된 Project 폴더로 이동

```bash
$ npx create-next-app@latest
```

##### 기본적으로 위의 코드를 사용하는게 맞는데 [NextJs Tutorial](https://nextjs.org/docs/getting-started/installation)에서는 이와 같이 설명

```bash
$ npx create-next-app@latest nextjs-dashboard --use-npm --example "https://github.com/vercel/next-learn/tree/main/dashboard/starter-example"
$ cd nextjs-dashboard
```

<br />

#### Folder 구조
---
- `/app`: Application에 대한 모든 경로, 구성 요소 및 논리가 포함됨(주 작업 장소)
- `/app/lib`: 재사용 가능한 Util 함수, 주로 Application에서 사용되는 함수가 포함
- `/app/ui`: Card, Table, Format등 UI 구성 요소 포함 / Bootstrap 형식
- `/public`: Static File(Images) 보관용
- `/script`: Seed Script(DB Conn) - 주로 nextjs로 db를 작업하는 것보다 nestjs를 연동하여 db 작업을 하는게 좀 더 효율성이 좋다.
- `Config file` Application Root에 next.config.js와 같은 Config File이 있다. 이 파일은 대부분 create-next-app을 사용하여 새 프로젝트를 시작할때 생성되고 사전 구성된다.

<br />

