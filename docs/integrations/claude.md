# Claude connector (remote MCP)

Kavel runs a remote MCP server at `https://www.kavel.ai/api/mcp`. Add it to Claude as a connector and
Claude can find a Kavel photo or video effect, generate or edit an image on your Kavel account, and
check your credit balance, all from a conversation.

## Add it

In Claude, open **Settings → Connectors → Add custom connector**, name it Kavel and paste the URL
above. Searching the effect catalog works without signing in. The first time Claude generates an
image it asks you to sign in to Kavel and approve the connection (OAuth). You can disconnect at any
time from the same settings page.

## Tools

| Tool | What it does | Sign-in |
|---|---|---|
| `find_kavel_tool` | Searches Kavel's effects (hairstyle changer, figurine, pet portrait, yearbook photo, trend dance videos and more) and returns each one's slug, whether it needs a photo, and its page on kavel.ai. | No |
| `generate_kavel_image` | Creates an image from a prompt, or edits an attached photo, optionally using an effect's tuned recipe (`tool`). Spends credits from your Kavel account. Usually returns the image within a minute; otherwise it returns a task id. | Yes |
| `check_kavel_generation` | Gets the result of a generation that was still rendering. | Yes |
| `get_kavel_balance` | Shows how many credits are left on your linked account. | Yes |

Only `generate_kavel_image` changes anything: it starts a generation and spends credits. Video effects
open on kavel.ai rather than running inside Claude.

## Credits and plans

Generations are paid with the credits on your Kavel account, the same as on the website. See
[pricing](https://www.kavel.ai/pricing?utm_source=readthedocs&utm_medium=claude) for what each plan includes.
Browse every effect at [kavel.ai/image](https://www.kavel.ai/image?utm_source=readthedocs&utm_medium=claude)
and [kavel.ai/video](https://www.kavel.ai/video?utm_source=readthedocs&utm_medium=claude).

## Data and privacy

The connector receives the prompts and photos you ask Claude to use for a generation, plus your account
email and name through sign-in. They are handled under the
[Kavel privacy policy](https://www.kavel.ai/privacy-policy). Disconnecting the connector stops any further
access.

## Support

Email [support@kavel.ai](mailto:support@kavel.ai).
