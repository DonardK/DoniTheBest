# Set up Lumen

Lumen plays movies and series from a magnet link, a torrent URL, or a `.torrent` file. Posters, title search, and downloaded English subtitles need three things you create yourself. This copy of Lumen does not include anyone else's keys.

You are responsible for the legality of anything you download. Use Lumen only for content you own or that you are allowed to download where you live.

## Install Lumen

Download `Lumen-0.1.0-setup.exe` from the **Releases** page of the GitHub repository. The installer is not in the file list. GitHub rejects files larger than 100 MB, and this installer is about 221 MB.

1. Run `Lumen-0.1.0-setup.exe`.
2. If Windows says **Windows protected your PC**, choose **More info**, then **Run anyway**. The installer is not signed by Microsoft. That warning is expected.
3. Leave the install folder as it is, and finish the installer.
4. Open **Lumen** from the desktop shortcut or the Start menu.

You do not need an administrator password. Lumen installs for your Windows user only.

Playback works before any of the steps below. Paste a magnet link into the bar at the top and press play. The three accounts below add posters, search, and extra subtitles.

## Where the keys go

Open Lumen, then the gear icon. Each box saves as you type. Choose **Done** when you are finished.

| Box in Settings | What to paste |
| --- | --- |
| TMDB API key | The v3 key from The Movie Database |
| Prowlarr address | Leave empty if Prowlarr is on this PC at the default port. Otherwise `http://127.0.0.1:` plus the port Prowlarr shows |
| Prowlarr API key | The key from Prowlarr's own settings |
| OpenSubtitles API key | The consumer API key from OpenSubtitles.com |

Keys stay on this PC, in your user account. Uninstalling Lumen does not delete them.

## TMDB (posters and titles)

TMDB turns a torrent name into a clean title, a year, a poster, and episode names. Without it, Lumen still plays the file and shows the raw torrent name.

1. Create a free account at [https://www.themoviedb.org/signup](https://www.themoviedb.org/signup).
2. Open the confirmation email and confirm the account.
3. Sign in, then open [https://www.themoviedb.org/settings/api](https://www.themoviedb.org/settings/api).
4. Choose **Request an API Key**, then **Developer**.
5. For the application name, type `Lumen`. For the application URL, type `http://localhost`. In the summary, say it is a personal player on your PC.
6. Submit the form. On the next page, copy **API Key (v3 auth)**. It is a short key of letters and numbers.
7. Paste that key into **TMDB API key** in Lumen.

Leave the long **API Read Access Token** alone. Lumen does not use it.

Add a movie or series again after the key is saved if the card still has no poster. Lumen fetches the poster the next time that title is added or refreshed.

## Prowlarr (search by title)

Prowlarr is a separate program. It runs on your PC and looks up torrent links when you type a title into Lumen. Lumen does not include Prowlarr, and it cannot use a Prowlarr that is installed on someone else's computer.

Search still needs at least one indexer inside Prowlarr. Add only indexers you are allowed to use. This guide does not list any.

1. Download the Windows installer from [https://prowlarr.com](https://prowlarr.com). Choose the 64-bit installer.
2. Run it and finish the install. Start Prowlarr if it does not open by itself.
3. In a browser, open [http://127.0.0.1:9696](http://127.0.0.1:9696). That page is Prowlarr, not Lumen.
4. In Prowlarr, open **Settings**, then **General**. Copy the **API Key**.
5. In Prowlarr, open **Indexers**, then **Add Indexer**, and add an indexer you are allowed to use. Save it and test it from that page.
6. In Lumen's Settings, paste the key into **Prowlarr API key**.
7. Leave **Prowlarr address** empty when the browser address is `http://127.0.0.1:9696`. If you changed Prowlarr's port, paste the full address, including `http://`, into **Prowlarr address**.

Prowlarr has to be running before a title search works. Open [http://127.0.0.1:9696](http://127.0.0.1:9696) if a search says it cannot reach Prowlarr. A magnet link does not need Prowlarr.

## OpenSubtitles (English subtitles)

Lumen looks for English subtitles in this order:

1. A subtitle file inside the torrent for that episode.
2. An English text subtitle embedded in the video.
3. OpenSubtitles, only when the first two have nothing and an API key is saved.

Other languages are ignored. Picture-based subtitles (PGS and VobSub) are ignored.

1. Create a free account at [https://www.opensubtitles.com](https://www.opensubtitles.com).
2. Confirm the email, then sign in.
3. Open the consumer API page: [https://www.opensubtitles.com/consumers](https://www.opensubtitles.com/consumers). From the account menu this is **Consumers**.
4. Create a consumer. Name it `Lumen`.
5. Copy that consumer's **API key**.
6. Paste it into **OpenSubtitles API key** in Lumen.

Use the key from OpenSubtitles.com. An older key from OpenSubtitles.org will not work.

The free account has a daily download limit set by OpenSubtitles. Subtitles that are already inside the torrent do not use that quota. The **CC** button and the `C` key turn captions on and off.

## Check that it works

1. Gear icon: all three boxes you care about are filled. Choose **Done**.
2. Type a title you are allowed to fetch and press Enter. Results mean Prowlarr is running, the key matches, and an indexer answered.
3. Play one result, or paste a magnet. After a short wait, the card should show a poster and a clean title. That means TMDB is working.
4. If the video has no English subtitle of its own, turn captions on. English text from OpenSubtitles appears when a match exists.

## When something fails

| What you see | What to do |
| --- | --- |
| Windows blocks the installer | **More info**, then **Run anyway** |
| Title search finds nothing | Open [http://127.0.0.1:9696](http://127.0.0.1:9696). Prowlarr must be running, the API key must match, and at least one indexer must be added and working |
| "Prowlarr address is not a valid URL" | Use `http://127.0.0.1:9696`, or leave the address box empty for that default |
| No poster | Paste the short TMDB **API Key (v3 auth)**, then add the title again |
| No downloaded subtitles | Paste the OpenSubtitles.com consumer key. A torrent that already contains English subtitles does not need it |
| Captions for the wrong episode | Lumen refuses a subtitle when the episode does not match. No captions is the safer result |
