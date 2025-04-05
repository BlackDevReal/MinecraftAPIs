
# 🌍 Unofficial Minecraft API Directory

A curated list of **unofficial Minecraft APIs** that provide player data, skins, server status, mods, and more. These are not affiliated with Mojang or Microsoft.

## 🧑 Player Info, Skins, UUIDs

### PlayerDB
- URL: `https://playerdb.co/api/player/minecraft/<username>`
- Description: UUID, name history, and skin info.

### MCHeads
- URL: `https://mc-heads.net/avatar/<username_or_uuid>`
- Description: Skin renders, avatars.

### Crafatar
- URL: `https://crafatar.com/avatars/<uuid>`
- Description: CDN for skins and avatars.

### Visage
- URL: `https://visage.surgeplay.com/face/<uuid>`
- Description: Full 3D renders of heads and skins.

### Ashcon API
- URL: `https://api.ashcon.app/mojang/v2/user/<username>`
- Description: Clean profile, UUID, skin.

## 🛰️ Server Status APIs

### MCStatus.io
- URL: `https://api.mcstatus.io/v2/status/java/<ip>`
- Description: Online status, version, player count.

### MCSrvStat.us
- URL: `https://api.mcsrvstat.us/2/<ip>`
- Description: Server data, MOTD, favicon.

## 📦 Modding & Launcher APIs

### Modrinth API
- URL: `https://api.modrinth.com/v2/`
- Description: Search mods, get download info.

### Spiget API
- URL: `https://api.spiget.org/v2/resources`
- Description: Spigot plugin data.

### CurseForge API
- URL: `https://api.curseforge.com/`
- Description: Mods, modpacks, textures.

## ☕ Java Example: Fetch UUID from PlayerDB

See `MinecraftAPIExample.java` in the `src/` folder for a working example using native Java HTTP and `org.json`.

---

_Disclaimer: All APIs listed here are community-maintained or reverse-engineered. Use at your own risk and follow each provider's usage policy._

## ☕ Java Example: Fetch UUID from PlayerDB

This example uses `HttpURLConnection` and the `org.json` library to query the PlayerDB API.

```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;
import org.json.JSONObject;

public class MinecraftAPIExample {
    public static void main(String[] args) {
        try {
            String username = "Notch"; // Replace with any username
            String endpoint = "https://playerdb.co/api/player/minecraft/" + username;

            URL url = new URL(endpoint);
            HttpURLConnection con = (HttpURLConnection) url.openConnection();
            con.setRequestMethod("GET");

            BufferedReader in = new BufferedReader(
                new InputStreamReader(con.getInputStream())
            );
            String inputLine;
            StringBuffer content = new StringBuffer();
            while ((inputLine = in.readLine()) != null) {
                content.append(inputLine);
            }

            in.close();
            con.disconnect();

            // Parse JSON response
            JSONObject response = new JSONObject(content.toString());
            String uuid = response.getJSONObject("data").getJSONObject("player").getString("id");
            System.out.println("UUID of " + username + ": " + uuid);

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

> Requires the `org.json` library. You can add it using Maven:
> 
> ```xml
> <dependency>
>   <groupId>org.json</groupId>
>   <artifactId>json</artifactId>
>   <version>20230227</version>
> </dependency>
> ```

---

## ☕ Java Example: Fetch UUID

```java
// Java code to get player UUID from an API
// Use HttpURLConnection or HttpClient
```

## 🐍 Python Example: Server Status Check

```python
# Use requests to get status from MCStatus.io or MCSrvStat.us
import requests
response = requests.get("https://api.mcstatus.io/v2/status/java/example.com")
print(response.json())
```

## 🌐 JavaScript (Node.js) Example: Fetch Skin

```javascript
// Use fetch or axios to get avatar from Crafatar
const fetch = require("node-fetch");
fetch("https://crafatar.com/avatars/player-uuid")
  .then(res => res.buffer())
  .then(buffer => require("fs").writeFileSync("avatar.png", buffer));
```

## 🧰 Curl Example

```bash
curl https://playerdb.co/api/player/minecraft/Notch
```
