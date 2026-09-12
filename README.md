# Mobbin Skills

Two complementary agent skills for researching shipped product interfaces with
[Mobbin](https://mobbin.com) and turning those references into polished,
native-feeling mobile experiences.

> [!IMPORTANT]
> This is an independent, community-maintained project. It is not affiliated
> with, endorsed by, or sponsored by Mobbin.

## The skills

| Skill | What it does |
|---|---|
| [`mobbin-usage`](skills/mobbin-usage/SKILL.md) | The research method: search Mobbin screens, flows, and website sections; inspect the actual images; preserve durable links; synthesize patterns; and build from evidence. |
| [`mobbin-app-design-skill`](skills/mobbin-app-design-skill/SKILL.md) | The implementation bar: native-feeling Expo and React Native screens, semantic colors, native controls, disciplined navigation and motion, complete states, and a simulator-verified finish. |

They are designed as a pair: `mobbin-usage` decides what to study, while
`mobbin-app-design-skill` defines how to build and verify the result.

## Install

From a project root:

```bash
npx skills@latest add AragornAms/mobbin-skills
```

Install just one skill:

```bash
npx skills@latest add AragornAms/mobbin-skills --skill mobbin-usage
npx skills@latest add AragornAms/mobbin-skills --skill mobbin-app-design-skill
```

For a user-wide installation:

```bash
npx skills@latest add AragornAms/mobbin-skills -g
```

<details>
<summary>Manual installation</summary>

Skills are plain directories. Copy them into the skills directory used by your
agent:

```bash
git clone https://github.com/AragornAms/mobbin-skills.git
cp -R mobbin-skills/skills/* ~/.claude/skills/
```

</details>

## Connect the Mobbin MCP

The research skill uses Mobbin's official hosted MCP server:

```text
https://api.mobbin.com/mcp
```

Add that URL as a Streamable HTTP MCP server in your client. On first use, your
client should open Mobbin's OAuth sign-in flow. Mobbin currently documents MCP
access for Pro, Team, and Enterprise plans.

Official setup instructions: [docs.mobbin.com/mcp](https://docs.mobbin.com/mcp)

## Try it

> Build me a habit tracker. Study relevant Mobbin onboarding and home screens
> first, then keep iterating until the full flow holds up in the simulator.

> Improve this screen. Diagnose the biggest hierarchy and interaction problems,
> find shipped references that solve them, and verify the revision on-device.

> Compare how strong fitness apps structure onboarding, including permission
> timing, personalization, navigation presentation, and paywall placement.

## Attribution and license

This repository is adapted from
[Appllama's `appllama-skills`](https://github.com/Appllama/appllama-skills),
which is available under the MIT License. The original copyright and license
notice are preserved in [LICENSE](LICENSE), and adaptation details are recorded
in [NOTICE](NOTICE).

Mobbin is a trademark of its respective owner. This license covers the code and
documentation in this repository; it does not grant rights to Mobbin's name,
logo, service, or content.

