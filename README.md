# ha-mcp 速查表 | ha-mcp Cheatsheet | Guía rápida de ha-mcp

**官方内置版只能替你开灯，这张能替你把「开灯的自动化」写出来——但它要的是管理员令牌，先看安全卡，再决定交不交**

> 一页看懂 homeassistant-ai/ha-mcp：Home Assistant 的一个 MCP 服务，把 Claude、ChatGPT 等 AI 助手接进你的智能家居。它给 AI 的是 87 个工具：不只查状态、开灯，还能创建与修改自动化、搭仪表盘卡片、装 HACS 集成、查错误日志——动的是配置层。它和 Home Assistant 官方内置的 MCP 不是一回事，区别就在下面第二张卡里。

- 上游项目：[homeassistant-ai/ha-mcp](https://github.com/homeassistant-ai/ha-mcp)（2026-11-11 实测 7,098 ★ / 446 forks；157 个 release、3,490 个 commit；2025-09-14 建仓）
- 平台：Home Assistant（进程内集成需 2026.8.0 以上）；工具数 87 个为原仓徽章口径
- 本页结构：中文主文 → English → Español → Português

---

Apoyo y más: [GitHub Sponsors](https://github.com/sponsors/Ezra-Zhao) · [Gumroad — plantillas y cuadernos que uso](https://ezraflow28.gumroad.com) · [Ko-fi](https://ko-fi.com/ezra777zhao)

## 安全卡（第一屏，这张是本页的命门）

ha-mcp 要的是**管理员级访问令牌**。把令牌交出去，等于把全屋的钥匙交给 AI。接之前先做完这四件事：

| 先做 | 为什么 |
|---|---|
| 先备份，再接 | 它能改自动化、改配置。手里有备份，改坏了能退回去 |
| 新建一个只给 ha-mcp 用的本地管理员账号 | 别用你的主账号令牌。专用账号一旦出事，可以单独吊销，不连累主账号 |
| Secret URL 不可外传 | 这条 URL 本身就是凭证，不是一条普通链接。谁拿到，谁就能连进你家 |
| 只装一种方式 | 四条装法选一条就好。同一个客户端挂两个入口，是已知的卡死原因（原仓口径） |

## 与官方内置 MCP 的分工卡（别搞混，这是两回事）

| | 官方内置 MCP | ha-mcp |
|---|---|---|
| 基于什么 | Home Assistant 的 Assist | 独立的 MCP 服务 |
| 主要管什么 | 控制**已暴露的实体**：查状态、开灯、调温度这类日常操作 | **配置层**：写自动化、改配置、管集成、搭仪表盘、查日志 |
| 一句话 | 替你操作家里已经有的东西 | 替你把「东西怎么自动运行」本身写出来 |

西语圈现有的指南大多只讲官方内置版；这张速查的独占价值，就是把 ha-mcp 这条配置层的路单独讲清。

## 四条装法，先选哪条

| 装法 | 怎么装 | 适合谁 |
|---|---|---|
| 进程内集成（首选） | HA 2026.11 起，直接在内置 Marketplace 里装；2026.8 至 2026.10 走 HACS | 全部安装类型都能用，最省事 |
| App 附加组件版 | HA OS 与 Supervised 用 App 版 | 免管 token，不想碰令牌配置的人 |
| Docker 或 uvx | 容器与 Core 安装走 Docker，或用 uvx 拉起 | 自己管运行环境的人 |
| stdio | 本地直连 | **只作演示**：原仓自述有已知传输问题，不推荐正式使用 |

（再提醒一次安全卡：四条里只选一条装，不要叠。）

## 版本门槛卡

- 进程内集成需要 Home Assistant **2026.8.0 以上**；版本不够，先升级 HA 再装。
- 自 v7.3.0 起，`ha_config_set_yaml` 已挪到 beta 频道——在稳定版里找不到这个工具，不是你装错了。

## 小模型一行版

- 用本地小模型或 Ollama 驱动时，要打开**搜索式工具发现**，别一次把 87 个工具全塞进上下文：小模型扛不住，选工具也会选错。

## 诚实标注区

- **体量**：7,098 ★ / 446 forks、157 个 release、3,490 个 commit（2026-11-11 原仓页实测，证据 A）；工具数 87 个为原仓徽章口径。
- **势头**：今日日榜第 3、约 +790 星/天（第三方榜单口径，证据 B）。本期三张里它体量最小、增速最猛。
- **装法时效**：西语已有一篇约 72 天前的长文教程，里面的工具数与装法都已过时（现行首选装法是 HA 2026.11 内置 Marketplace）；本页装法以 2026-11-11 的原仓口径为准。
- **安全再说一遍**：管理员令牌等于全屋权限。先备份、用专用账号、Secret URL 不外传——三条没做到，先别接。

---

## English (summary)

ha-mcp (7,098 stars / 446 forks as of 2026-11-11; 157 releases) is an MCP server for Home Assistant that connects AI assistants such as Claude and ChatGPT to your smart home with 87 tools. It goes beyond checking state and switching lights: the AI can create and edit automations, build dashboard cards, install HACS integrations and read error logs — it works at the configuration layer. Safety card, first and non-negotiable: ha-mcp needs an admin-level access token, and that token is the keys to your whole house. Back up before you connect anything; create a dedicated local admin account used only by ha-mcp, so it can be revoked on its own; the Secret URL is itself a credential — never share it; and install exactly one method, because attaching the same client through two endpoints is a known cause of freezes (upstream's own note). Not the same as Home Assistant's official built-in MCP: the official one is based on Assist and mainly controls entities you have exposed, while ha-mcp manages the configuration layer — writing the automations themselves. Four install paths: the in-process integration is the recommended one (built-in Marketplace from HA 2026.11; via HACS for 2026.8–2026.10; works on all install types); the App add-on for HA OS and Supervised, which avoids manual token handling; Docker or uvx for container and Core installs; stdio is demo-only, as upstream notes known transport issues. Version gates: the in-process integration needs Home Assistant 2026.8.0 or newer, and since v7.3.0 `ha_config_set_yaml` lives on the beta channel. With local small models or Ollama, enable search-based tool discovery instead of stuffing all 87 tools into the context.

---

## Español (guía rápida — traducción de estudio, pendiente de revisión por un hablante nativo)

**La versión oficial integrada solo puede encenderte la luz; esta puede escribir por ti la automatización que la enciende. Pero pide un token de administrador: mira primero la tarjeta de seguridad antes de entregarlo.**

Tarjeta de seguridad (lo primero, y es lo más importante de esta página): ha-mcp necesita un token de acceso de nivel administrador, y ese token equivale a las llaves de toda tu casa. Haz una copia de seguridad antes de conectar nada. Crea una cuenta de administrador local nueva, solo para ha-mcp: si algo sale mal, la revocas sin tocar tu cuenta principal. La URL secreta es en sí misma una credencial, no un enlace cualquiera: no la compartas. E instala una sola vía de acceso: conectar el mismo cliente por dos entradas es una causa conocida de bloqueos, según el propio repositorio original.

No es lo mismo que el MCP oficial integrado de Home Assistant. El oficial se basa en Assist y controla sobre todo las entidades que ya tienes expuestas — consultar estados, encender luces —. ha-mcp trabaja en la capa de configuración: escribe automatizaciones, cambia la configuración, gestiona integraciones, arma tarjetas de panel y revisa los registros de errores. Dicho corto: el oficial opera lo que ya existe; ha-mcp escribe cómo se comporta tu casa.

ha-mcp (7.098 estrellas / 446 forks a 11 de noviembre de 2026; 157 releases) le da al asistente 87 herramientas según el distintivo del repositorio original. Cuatro vías de instalación, elige una: la integración en proceso es la recomendada — desde HA 2026.11 se instala directo en el Marketplace integrado, y entre 2026.8 y 2026.10 se instala por HACS; sirve para todo tipo de instalación —; la versión App para HA OS y Supervised, que evita manejar tokens a mano; Docker o uvx para instalaciones en contenedor o Core; y stdio solo como demostración, porque el repositorio original reconoce problemas conocidos de transporte y no lo recomienda para uso serio. Requisitos de versión: la integración en proceso pide Home Assistant 2026.8.0 o superior, y desde la v7.3.0 la herramienta `ha_config_set_yaml` pasó al canal beta. Si usas un modelo local pequeño u Ollama, activa el descubrimiento de herramientas por búsqueda: no metas las 87 herramientas de golpe en el contexto.

---

## Português (guia rápido — tradução de estudo, aguardando revisão de um falante nativo)

**A versão oficial integrada só consegue acender a luz para você; esta consegue escrever a automação que acende a luz. Mas ela pede um token de administrador: olhe primeiro o cartão de segurança antes de entregar.**

Cartão de segurança (o primeiro, e é o mais importante desta página): o ha-mcp precisa de um token de acesso de nível administrador, e esse token equivale às chaves da sua casa inteira. Faça backup antes de conectar qualquer coisa. Crie uma conta de administrador local nova, só para o ha-mcp: se algo der errado, você revoga só ela, sem tocar na sua conta principal. A URL secreta é, ela mesma, uma credencial, não um link qualquer: não compartilhe. E instale uma única via de acesso: conectar o mesmo cliente por duas entradas é uma causa conhecida de travamento, segundo o próprio repositório original.

Não é a mesma coisa que o MCP oficial integrado do Home Assistant. O oficial é baseado no Assist e controla principalmente as entidades que você já expôs — consultar estados, acender luzes —. O ha-mcp trabalha na camada de configuração: escreve automações, altera a configuração, gerencia integrações, monta cartões de painel e lê os registros de erro. Resumindo: o oficial opera o que já existe; o ha-mcp escreve como a sua casa se comporta.

O ha-mcp (7.098 estrelas / 446 forks em 11 de novembro de 2026; 157 releases) entrega ao assistente 87 ferramentas, pelo selo do repositório original. Quatro vias de instalação, escolha uma: a integração em processo é a recomendada — a partir do HA 2026.11, instala direto no Marketplace integrado; entre 2026.8 e 2026.10, instala pelo HACS; serve para todos os tipos de instalação —; a versão App para HA OS e Supervised, que evita lidar com tokens na mão; Docker ou uvx para instalações em contêiner ou Core; e stdio só como demonstração, porque o repositório original reconhece problemas conhecidos de transporte e não recomenda para uso sério. Requisitos de versão: a integração em processo pede Home Assistant 2026.8.0 ou superior, e desde a v7.3.0 a ferramenta `ha_config_set_yaml` passou para o canal beta. Se você usa um modelo local pequeno ou o Ollama, ative a descoberta de ferramentas por busca: não coloque as 87 ferramentas de uma vez no contexto.

---

## 来源与声明

- 灵感来源 / Source / Fuente / Fonte: [homeassistant-ai/ha-mcp](https://github.com/homeassistant-ai/ha-mcp)（2026-11-11 实测 7,098 ★ / 446 forks，157 个 release）
- 本仓是个人学习整理：内容用我自己的话总结自上游公开文档，不搬运原文；装法、版本门槛与安全口径以 2026-11-11 的上游 README 为准，星数以同日 GitHub 实测为准，上游迭代后请以官方文档为最终依据。
- 西语、葡语部分为学习译稿，待母语校对。Las secciones en español y portugués son traducciones de estudio pendientes de revisión nativa.
- License: MIT © 2026 Guangyi Zhao
