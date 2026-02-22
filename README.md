<p align="right">
   <strong>中文</strong> 
</p>
<div align="center">

# kilo2api

_觉得有点意思的话 别忘了点个 ⭐_

<a href=https://t.me/+raL5ppEzDIFmZTY1">
  <img src="https://img.shields.io/badge/Telegram-AI Wave交流群-0088cc?style=for-the-badge&logo=telegram&logoColor=white" alt="Telegram 交流群" />
</a>

<sup><i>AI Wave 社群</i></sup> · <sup><i>(群内提供公益API、AI机器人)</i></sup>


</div>

> 因一些原因暂未提交代码，但docker镜像一直在更新。

## 功能

- [x] 支持对话接口(流式/非流式)(`/chat/completions`),详情查看[支持模型](#支持模型)
- [x] 支持识别**图片**多轮对话
- [x] 支持自定义请求头校验值(Authorization)
- [x] 支持cookie池(随机),详情查看[获取cookie](#cookie获取方式)
- [x] 支持请求失败自动切换cookie重试(需配置cookie池)
- [x] 可配置代理请求(环境变量`PROXY_URL`)

### 接口文档:

略

### 示例:

略

## 如何使用

略

## 如何集成NextChat

略

## 如何集成one-api

略

## 部署

### 基于 Docker-Compose(All In One) 进行部署

```shell
docker-compose pull && docker-compose up -d
```

#### docker-compose.yml

```docker
version: '3.4'

services:
  kilo2api:
    image: deanxv/kilo2api:latest
    container_name: kilo2api
    restart: always
    ports:
      - "7099:7099"
    volumes:
      - ./data:/app/kilo2api/data
    environment:
      - KL_COOKIE=******  # cookie (多个请以,分隔)
      - API_SECRET=123456  # [可选]接口密钥-修改此行为请求头校验的值(多个请以,分隔)
      - TZ=Asia/Shanghai
```

### 基于 Docker 进行部署

```docker
docker run --name kilo2api -d --restart always \
-p 7099:7099 \
-v $(pwd)/data:/app/kilo2api/data \
-e KL_COOKIE=***** \
-e API_SECRET="123456" \
-e TZ=Asia/Shanghai \
deanxv/kilo2api
```

其中`API_SECRET`、`KL_COOKIE`修改为自己的。

如果上面的镜像无法拉取,可以尝试使用 GitHub 的 Docker 镜像,将上面的`deanxv/kilo2api`替换为
`ghcr.io/deanxv/kilo2api`即可。

### 部署到第三方平台

<details>
<summary><strong>部署到 Zeabur</strong></summary>
<div>

[![Deployed on Zeabur](https://zeabur.com/deployed-on-zeabur-dark.svg)](https://zeabur.com?referralCode=deanxv&utm_source=deanxv)

> Zeabur 的服务器在国外,自动解决了网络的问题,~~同时免费的额度也足够个人使用~~

1. 首先 **fork** 一份代码。
2. 进入 [Zeabur](https://zeabur.com?referralCode=deanxv),使用github登录,进入控制台。
3. 在 Service -> Add Service,选择 Git（第一次使用需要先授权）,选择你 fork 的仓库。
4. Deploy 会自动开始,先取消。
5. 添加环境变量

   `KL_COOKIE:******`  cookie (多个请以,分隔)

   `API_SECRET:123456` [可选]接口密钥-修改此行为请求头校验的值(多个请以,分隔)(与openai-API-KEY用法一致)

保存。

6. 选择 Redeploy。

</div>


</details>

<details>
<summary><strong>部署到 Render</strong></summary>
<div>

> Render 提供免费额度,绑卡后可以进一步提升额度

Render 可以直接部署 docker 镜像,不需要 fork 仓库：[Render](https://dashboard.render.com)

</div>
</details>

## 配置

### 环境变量

1. `PORT=7099`  [可选]端口,默认为7099
2. `DEBUG=true`  [可选]DEBUG模式,可打印更多信息[true:打开、false:关闭]
3. `API_SECRET=123456`  [可选]接口密钥-修改此行为请求头(Authorization)校验的值(同API-KEY)(多个请以,分隔)
4. `KL_COOKIE=******`  cookie (多个请以,分隔)
5. `REQUEST_RATE_LIMIT=60`  [可选]每分钟下的单ip请求速率限制,默认:60次/min
6. `PROXY_URL=http://127.0.0.1:10801`  [可选]代理
6. `USER_AGENT=Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome`  [可选]请求标识,用自己的(可能)防封,默认使用作者的。
7. `ROUTE_PREFIX=hf`  [可选]路由前缀,默认为空,添加该变量后的接口示例:`/hf/v1/chat/completions`
8. `RATE_LIMIT_COOKIE_LOCK_DURATION=600`  [可选]到达速率限制的cookie禁用时间,默认为60s

### cookie获取方式

1. 打开[kilocode](https://kilocode.ai/profile)。
2. 打开**F12**开发者工具。
3. 使用Google登录
<span><img src="docs/img.png" width="800"/></span>
4. 右侧开发者工具-控制台，执行如下代码。

```
document.querySelector('a[href^="vscode://kilocode.kilo-code/kilocode?token="]').href.split('token=')[1]
```

5. 打印的值即所需cookie值,即环境变量`KL_COOKIE`。
<span><img src="docs/img2.png" width="800"/></span>

## 进阶配置

略

## 支持模型

> 新用户注册送$5额度，绑卡价送 $15。

<details>
<summary>点击展开完整模型列表</summary>

| 模型名称                                    |
|-----------------------------------------|
| claude-3.7-sonnet                       |
| claude-3.7-sonnet:thinking              |
| gpt-4.1                                 |
| gemini-2.5-flash-preview                |
| claude-opus-4                           |
| claude-sonnet-4                         |
| devstral-small:free                     |
| devstral-small                          |
| gemma-3n-e4b-it:free                    |
| gemini-2.5-flash-preview-05-20          |
| gemini-2.5-flash-preview-05-20:thinking |
| codex-mini                              |
| llama-3.3-8b-instruct:free              |
| deephermes-3-mistral-24b-preview:free   |
| mistral-medium-3                        |
| gemini-2.5-pro-preview                  |
| caller-large                            |
| spotlight                               |
| maestro-reasoning                       |
| virtuoso-large                          |
| coder-large                             |
| virtuoso-medium-v2                      |
| arcee-blitz                             |
| phi-4-reasoning-plus:free               |
| phi-4-reasoning-plus                    |
| phi-4-reasoning:free                    |
| mercury-coder-small-beta                |
| qwen3-4b:free                           |
| internvl3-14b:free                      |
| internvl3-2b:free                       |
| deepseek-prover-v2:free                 |
| deepseek-prover-v2                      |
| llama-guard-4-12b                       |
| qwen3-30b-a3b:free                      |
| qwen3-30b-a3b                           |
| qwen3-8b:free                           |
| qwen3-8b                                |
| qwen3-14b:free                          |
| qwen3-14b                               |
| qwen3-32b:free                          |
| qwen3-32b                               |
| qwen3-235b-a22b:free                    |
| qwen3-235b-a22b                         |
| deepseek-r1t-chimera:free               |
| glm-z1-rumination-32b                   |
| glm-z1-9b:free                          |
| glm-4-9b:free                           |
| mai-ds-r1:free                          |
| glm-z1-32b:free                         |
| glm-z1-32b                              |
| glm-4-32b:free                          |
| glm-4-32b                               |
| gemini-2.5-flash-preview:thinking       |
| o4-mini-high                            |
| o3                                      |
| o4-mini                                 |
| shisa-v2-llama3.3-70b:free              |
| qwen2.5-coder-7b-instruct               |
| gpt-4.1-mini                            |
| gpt-4.1-nano                            |
| llemma_7b                               |
| codellama-7b-instruct-solidity          |
| qwq-32b-arliai-rpr-v1:free              |
| deepcoder-14b-preview:free              |
| kimi-vl-a3b-thinking:free               |
| grok-3-mini-beta                        |
| grok-3-beta                             |
| llama-3.3-nemotron-super-49b-v1:free    |
| llama-3.3-nemotron-super-49b-v1         |
| llama-3.1-nemotron-ultra-253b-v1:free   |
| llama-4-maverick:free                   |
| llama-4-maverick                        |
| llama-4-scout:free                      |
| llama-4-scout                           |
| openhands-lm-32b-v0.1                   |
| deepseek-v3-base:free                   |
| llama3.1-typhoon2-8b-instruct           |
| llama3.1-typhoon2-70b-instruct          |
| qwen2.5-vl-3b-instruct:free             |
| gemini-2.5-pro-exp-03-25                |
| qwen2.5-vl-32b-instruct:free            |
| qwen2.5-vl-32b-instruct                 |
| deepseek-chat-v3-0324:free              |
| deepseek-chat-v3-0324                   |
| qwerky-72b:free                         |
| o1-pro                                  |
| mistral-small-3.1-24b-instruct:free     |
| mistral-small-3.1-24b-instruct          |
| olympiccoder-32b:free                   |
| gemma-3-1b-it:free                      |
| gemma-3-4b-it:free                      |
| gemma-3-4b-it                           |
| jamba-1.6-large                         |
| jamba-1.6-mini                          |
| gemma-3-12b-it:free                     |
| gemma-3-12b-it                          |
| command-a                               |
| gpt-4o-mini-search-preview              |
| gpt-4o-search-preview                   |
| reka-flash-3:free                       |
| gemma-3-27b-it:free                     |
| gemma-3-27b-it                          |
| anubis-pro-105b-v1                      |
| skyfall-36b-v2                          |
| phi-4-multimodal-instruct               |
| sonar-reasoning-pro                     |
| sonar-pro                               |
| sonar-deep-research                     |
| deepseek-r1-zero:free                   |
| qwq-32b:free                            |
| qwq-32b                                 |
| moonlight-16b-a3b-instruct:free         |
| deephermes-3-llama-3-8b-preview:free    |
| gpt-4.5-preview                         |
| gemini-2.0-flash-lite-001               |
| claude-3.7-sonnet:beta                  |
| r1-1776                                 |
| mistral-saba                            |
| dolphin3.0-r1-mistral-24b:free          |
| dolphin3.0-mistral-24b:free             |
| llama-guard-3-8b                        |
| o3-mini-high                            |
| deepseek-r1-distill-llama-8b            |
| gemini-2.0-flash-001                    |
| qwen-vl-plus                            |
| aion-1.0                                |
| aion-1.0-mini                           |
| aion-rp-llama-3.1-8b                    |
| qwen-vl-max                             |
| qwen-turbo                              |
| qwen2.5-vl-72b-instruct:free            |
| qwen2.5-vl-72b-instruct                 |
| qwen-plus                               |
| qwen-max                                |
| o3-mini                                 |
| deepseek-r1-distill-qwen-1.5b           |
| mistral-small-24b-instruct-2501:free    |
| mistral-small-24b-instruct-2501         |
| deepseek-r1-distill-qwen-32b:free       |
| deepseek-r1-distill-qwen-32b            |
| deepseek-r1-distill-qwen-14b:free       |
| deepseek-r1-distill-qwen-14b            |
| sonar-reasoning                         |
| sonar                                   |
| lfm-7b                                  |
| lfm-3b                                  |
| deepseek-r1-distill-llama-70b:free      |
| deepseek-r1-distill-llama-70b           |
| deepseek-r1:free                        |
| deepseek-r1                             |
| minimax-01                              |
| codestral-2501                          |
| phi-4                                   |
| deepseek-chat:free                      |
| deepseek-chat                           |
| l3.3-euryale-70b                        |
| o1                                      |
| eva-llama-3.33-70b                      |
| grok-2-vision-1212                      |
| grok-2-1212                             |
| command-r7b-12-2024                     |
| gemini-2.0-flash-exp:free               |
| llama-3.3-70b-instruct:free             |
| llama-3.3-70b-instruct                  |
| nova-lite-v1                            |
| nova-micro-v1                           |
| nova-pro-v1                             |
| qwq-32b-preview                         |
| eva-qwen-2.5-72b                        |
| gpt-4o-2024-11-20                       |
| mistral-large-2411                      |
| mistral-large-2407                      |
| pixtral-large-2411                      |
| grok-vision-beta                        |
| mn-inferor-12b                          |
| qwen-2.5-coder-32b-instruct:free        |
| qwen-2.5-coder-32b-instruct             |
| sorcererlm-8x22b                        |
| eva-qwen-2.5-32b                        |
| unslopnemo-12b                          |
| claude-3.5-haiku:beta                   |
| claude-3.5-haiku                        |
| claude-3.5-haiku-20241022:beta          |
| claude-3.5-haiku-20241022               |
| llama-3.1-lumimaid-70b                  |
| magnum-v4-72b                           |
| claude-3.5-sonnet:beta                  |
| claude-3.5-sonnet                       |
| grok-beta                               |
| ministral-3b                            |
| ministral-8b                            |
| qwen-2.5-7b-instruct:free               |
| qwen-2.5-7b-instruct                    |
| llama-3.1-nemotron-70b-instruct         |
| inflection-3-productivity               |
| inflection-3-pi                         |
| gemini-flash-1.5-8b                     |
| magnum-v2-72b                           |
| rocinante-12b                           |
| lfm-40b                                 |
| llama-3.2-3b-instruct:free              |
| llama-3.2-3b-instruct                   |
| llama-3.2-90b-vision-instruct           |
| llama-3.2-1b-instruct:free              |
| llama-3.2-1b-instruct                   |
| llama-3.2-11b-vision-instruct:free      |
| llama-3.2-11b-vision-instruct           |
| qwen-2.5-72b-instruct:free              |
| qwen-2.5-72b-instruct                   |
| llama-3.1-lumimaid-8b                   |
| o1-mini-2024-09-12                      |
| o1-preview-2024-09-12                   |
| o1-mini                                 |
| o1-preview                              |
| pixtral-12b                             |
| command-r-08-2024                       |
| command-r-plus-08-2024                  |
| qwen-2.5-vl-7b-instruct:free            |
| qwen-2.5-vl-7b-instruct                 |
| l3.1-euryale-70b                        |
| phi-3.5-mini-128k-instruct              |
| hermes-3-llama-3.1-70b                  |
| hermes-3-llama-3.1-405b                 |
| chatgpt-4o-latest                       |
| mn-starcannon-12b                       |
| l3-lunaris-8b                           |
| gpt-4o-2024-08-06                       |
| mn-celeste-12b                          |
| llama-3.1-405b:free                     |
| llama-3.1-405b                          |
| llama-3.1-sonar-small-128k-online       |
| llama-3.1-sonar-large-128k-online       |
| llama-3.1-8b-instruct:free              |
| llama-3.1-8b-instruct                   |
| llama-3.1-405b-instruct                 |
| llama-3.1-70b-instruct                  |
| mistral-nemo:free                       |
| mistral-nemo                            |
| codestral-mamba                         |
| gpt-4o-mini                             |
| gpt-4o-mini-2024-07-18                  |
| gemma-2-27b-it                          |
| magnum-72b                              |
| gemma-2-9b-it:free                      |
| gemma-2-9b-it                           |
| yi-large                                |
| claude-3.5-sonnet-20240620:beta         |
| claude-3.5-sonnet-20240620              |
| l3-euryale-70b                          |
| dolphin-mixtral-8x22b                   |
| qwen-2-72b-instruct                     |
| mistral-7b-instruct:free                |
| mistral-7b-instruct                     |
| hermes-2-pro-llama-3-8b                 |
| mistral-7b-instruct-v0.3                |
| phi-3-mini-128k-instruct                |
| phi-3-medium-128k-instruct              |
| llama-3-lumimaid-70b                    |
| gemini-flash-1.5                        |
| deepseek-coder                          |
| llama-guard-2-8b                        |
| gpt-4o                                  |
| gpt-4o:extended                         |
| gpt-4o-2024-05-13                       |
| olmo-7b-instruct                        |
| llama-3-lumimaid-8b:extended            |
| llama-3-lumimaid-8b                     |
| fimbulvetr-11b-v2                       |
| llama-3-70b-instruct                    |
| llama-3-8b-instruct                     |
| mixtral-8x22b-instruct                  |
| wizardlm-2-8x22b                        |
| gpt-4-turbo                             |
| gemini-pro-1.5                          |
| command-r-plus                          |
| command-r-plus-04-2024                  |
| midnight-rose-70b                       |
| command                                 |
| command-r                               |
| claude-3-haiku:beta                     |
| claude-3-haiku                          |
| claude-3-sonnet:beta                    |
| claude-3-sonnet                         |
| claude-3-opus:beta                      |
| claude-3-opus                           |
| command-r-03-2024                       |
| mistral-large                           |
| gpt-3.5-turbo-0613                      |
| gpt-4-turbo-preview                     |
| nous-hermes-2-mixtral-8x7b-dpo          |
| mistral-small                           |
| mistral-medium                          |
| mistral-tiny                            |
| mistral-7b-instruct-v0.2                |
| mixtral-8x7b-instruct                   |
| noromaid-20b                            |
| claude-2.1:beta                         |
| claude-2.1                              |
| claude-2:beta                           |
| claude-2                                |
| toppy-m-7b                              |
| goliath-120b                            |
| auto                                    |
| gpt-4-1106-preview                      |
| gpt-3.5-turbo-1106                      |
| gpt-3.5-turbo-instruct                  |
| mistral-7b-instruct-v0.1                |
| mythalion-13b                           |
| gpt-4-32k-0314                          |
| gpt-3.5-turbo-16k                       |
| gpt-4-32k                               |
| weaver                                  |
| claude-2.0:beta                         |
| claude-2.0                              |
| remm-slerp-l2-13b                       |
| mythomax-l2-13b                         |
| llama-2-70b-chat                        |
| gpt-4-0314                              |
| gpt-4                                   |
| gpt-3.5-turbo-0125                      |
| gpt-3.5-turbo                           |

</details>

> 可通过下图获取并保存`__Secure-next-auth.session-token`随时在[kilo查询平台](https://kl.aytsao.cn/)查询余额。

<span><img src="docs/img1.png" width="400"/></span>

<span><img src="docs/img3.png" width="400"/></span>


## 报错排查

略

## 其他

略
