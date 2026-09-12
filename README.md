# Minion Control

A personal video production tool for one YouTube channel.

Minion Control is a single-user macOS tool written and operated by João David Frexes
Fragata Ferreira da Costa. It drafts a script, generates original diagrams and narration,
renders a video locally, and — only after the owner approves that exact rendered file —
uploads it to the owner's own YouTube channel. It then reads that channel's own analytics
to decide what to produce next.

It is not distributed, has no sign-up, and has no users other than its owner.

## How it uses the YouTube API

- `channels.list` (`mine=true`) — confirm the authorized channel and read the owner's own channel statistics
- `videos.insert` — upload the owner's own videos
- `videos.list` — verify the upload processed and its metadata matches what was approved
- `thumbnails.set` — set the thumbnail on the owner's own video
- YouTube Analytics `reports.query` — retention and views for the owner's own channel only

It does not read, index, store or display any other channel's or user's data, and it does
not search, scrape or aggregate YouTube content.

## Synthetic media disclosure

Narration and imagery are generated. Every upload sets `status.containsSyntheticMedia` on
the `videos.insert` call, so YouTube's altered-content disclosure is applied at upload time
rather than added afterwards. `selfDeclaredMadeForKids` is set explicitly on every upload;
the channel is general-audience and is not made for kids.

## Privacy policy

Minion Control collects no data from anyone other than its owner, because it has no other
users.

- The Google OAuth refresh token and client secret are stored in the macOS Keychain on a
  single machine. They are never transmitted to any server, browser or third party.
- Video IDs, upload status and the owner's own channel analytics are stored in a private
  database that only the owner can sign in to.
- No data obtained from the YouTube API is sold, shared, used for advertising, or disclosed
  to any third party.
- Revoking access at [Google Account permissions](https://myaccount.google.com/permissions),
  or deleting the Keychain entries, stops all API use immediately and destroys the stored
  credentials.

Governed by the [YouTube Terms of Service](https://www.youtube.com/t/terms) and the
[Google Privacy Policy](https://policies.google.com/privacy).

## Contact

joaodavidfffcosta@gmail.com
