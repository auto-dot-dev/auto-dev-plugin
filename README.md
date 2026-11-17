# Auto.dev

Ask Claude about any vehicle and get answers from live Auto.dev data. Decode a VIN, search cars
for sale, and pull photos, specifications, recalls, payment and interest-rate estimates, taxes
and fees, and total cost of ownership, without leaving the conversation.

## What's inside

- **The Auto.dev connector**, the hosted MCP server at `https://mcp.auto.dev/mcp`. It gives
  Claude 14 read-only tools. None of them changes your data.
- **The `vehicle-data` skill**, which tells Claude which tool answers which question, how to
  check a VIN before calling a tool, and how to explain plan limits.

## Get started

1. Add the plugin, then open its **Connectors** tab and connect **Auto.dev**. In Claude Code,
   run `/mcp` and choose **Authenticate** for `auto-dev`.
2. Sign in with your Auto.dev account, or create one. Sign-in happens on id.org.ai, the
   sign-in service Auto.dev uses. The Free plan needs no card.
3. Ask something like "Decode 2T3P1RFV5MW142204" or "Find 2021 to 2023 Toyota RAV4s under
   $30,000 in Texas".

## Plans and usage

VIN decode, listings, and photos work on every plan, including Free. Specs, build data, recalls,
payments, interest rates, and cost of ownership need Growth. Open recalls, plate-to-VIN, and
taxes and fees need Scale. Every tool call is an Auto.dev API request: it counts toward the
Free plan's 1,000 included calls, or is billed at your plan's per-call data rate on Growth and
Scale. One "everything about this car" request can make several calls. See
[pricing](https://www.auto.dev/pricing).

## Data

When Claude calls a tool, the plugin sends that tool's inputs, such as a VIN, search filters,
a ZIP code, a credit score, or a license plate you provide, to Auto.dev
through `mcp.auto.dev`. Auto.dev logs each request for billing and usage reporting. The plugin
itself stores nothing and sends nothing anywhere else. Read the
[privacy policy](https://www.auto.dev/privacy).

## Support

Email team@auto.dev, or read the
[documentation](https://docs.auto.dev/v2/mcp-quickstart).
