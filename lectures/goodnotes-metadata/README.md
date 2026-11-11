# CSDS 611 Goodnotes recordings

Extracted 17 unique audio clips totaling 17 h 32 min 28 s of playback. The four clips in the older Domain Drive snapshot match clips in the Personal Drive snapshot by attachment ID and SHA-256. All clips passed ZIP integrity, hash, stream, and full audio decode checks. The audio files contain the original member bytes with an added `.m4a` extension.

## Files

- [Recording inventory](recordings.csv) gives one row per unique clip.
- [Detailed metadata](recordings.json) preserves both source observations, including the older duplicate copies, raw event fields, replay anchors, media tags, and hashes.
- The [lecture directory](../README.md#recordings-by-date) holds the 17 original AAC-LC streams in MP4 containers, all mono at 22,050 Hz. The CSV and JSON retain paths from the original extraction layout.

## Dates and coverage

Dates use America/New_York, including the November change from EDT to EST. The app event time agrees with the media creation tag within about a second. It appears to mark finalization in these archives. Estimated start subtracts playback duration from that time.

The [course syllabus](../../CSDS_611_syllabus.pdf) schedules Tuesday and Thursday classes. Excluding October 6 and November 3, the [UT Knoxville academic calendar](https://registrar.utk.edu/wp-content/uploads/sites/4/2025/12/2026-2027-Published-Calendar.pdf) gives 22 possible slots between term start and November 5. No audio was found for 2026-08-18, 2026-09-15, 2026-10-15, 2026-10-20, 2026-10-22. These are schedule gaps in the recovered inventory. Whether each meeting took place is unverified.

The [lecture library](https://app.notion.com/p/341ee83111d3494594a421e2221c95fb) organizes numbered slide decks without a date mapping. The recovered clips are identified by recording date. Each audio file may cover only part of its meeting.

| Date | Playback | Estimated start (ET) | Replay anchors |
| --- | ---: | --- | ---: |
| [2026-08-20](../2026-08-20_FB8DE074.m4a) | 66:23 | 14:32:27 | 392 |
| [2026-08-25](../2026-08-25_3D786893.m4a) | 64:46 | 14:30:42 | 605 |
| [2026-08-27](../2026-08-27_0A2DB600.m4a) | 58:16 | 14:30:55 | 475 |
| [2026-09-01](../2026-09-01_D708E20C.m4a) | 67:01 | 14:31:10 | 338 |
| [2026-09-03](../2026-09-03_C995A7EF.m4a) | 59:27 | 14:32:40 | 256 |
| [2026-09-08](../2026-09-08_FE79D51A.m4a) | 66:58 | 14:32:26 | 734 |
| [2026-09-10](../2026-09-10_349E6F2E.m4a) | 65:44 | 14:31:35 | 95 |
| [2026-09-17](../2026-09-17_0EF7DF90.m4a) | 61:11 | 14:33:16 | 55 |
| [2026-09-22](../2026-09-22_0C09C6AA.m4a) | 48:10 | 14:33:44 | 423 |
| [2026-09-24](../2026-09-24_2C2C7B9F.m4a) | 76:26 | 14:32:10 | 103 |
| [2026-09-29](../2026-09-29_17950960.m4a) | 60:43 | 14:31:05 | 319 |
| [2026-10-01](../2026-10-01_9A3E8C58.m4a) | 51:14 | 14:30:58 | 61 |
| [2026-10-08](../2026-10-08_52291E85.m4a) | 60:12 | 14:31:27 | 33 |
| [2026-10-13](../2026-10-13_09627C3C.m4a) | 58:25 | 14:33:04 | 24 |
| [2026-10-27](../2026-10-27_0AF31E51.m4a) | 53:54 | 14:47:04 | 0 |
| [2026-10-29](../2026-10-29_B21AFBFC.m4a) | 64:10 | 14:31:57 | 281 |
| [2026-11-05](../2026-11-05_13D4A044.m4a) | 69:27 | 14:31:24 | 1030 |

## App metadata

The app duration-like field divided by one billion is 70.56% of playback duration for all 17 files. Both values are retained. Raw replay offsets have unverified playback units. The latest archive links all 5,224 replay anchors to page and note members through the search index. The October 27 clip has no replay anchors. No custom recording names or audio transcript payloads were positively identified.

## Drive sources

- [Personal Drive native archive](https://drive.google.com/file/d/1ic_BTvdAJffrtRD__oWWLj2CphcoqFmd/view) was updated on November 6, 2026.
- [Domain Drive native archive](https://drive.google.com/file/d/1JZPHLfvYTQ5zx3fIqFXH9_XbllBkOXGh/view) was updated on September 3, 2026.
- The UTK School account, including its accessible shared drives in connector search, produced no course notebook match. Direct folder listing exposed both native files in the other accounts.
