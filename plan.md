# আমার জেলা — Implementation Plan

## Product direction

“আমার জেলা” একটি বাংলা-first district travel memory card maker। উপরের tab navigation-এ **আমার জেলা ভ্রমণ**, **আমার সম্পর্কে** এবং পরবর্তী feature-এর জন্য **আরও আসছে** থাকবে। প্রথম release-এ district journey flow সম্পূর্ণ হবে; self-profile card পরে আলাদা discussion অনুযায়ী তৈরি হবে।

User প্রথমে initial ৮টি district-এর একটি select করবে। District select করার আগে visited-place list বা journey map দেখা যাবে না। District select করার পর শুধু সেই district-এর researched visitor places দেখাবে। User যে জায়গাগুলো select করবে, actual Bangladesh district-vector map-এ সেই place-এর approximate coordinate marker filled/coral হবে এবং label উঠবে; unselected places blank থাকবে।

User এরপর নিজের নাম/nickname, photo এবং signature dialogue যোগ করবে। Final card reference-style editorial map card হিসেবে district name, visited count, filled markers, place labels, photo এবং dialogue দেখাবে। PNG/JPG/PDF print এবং share/copy-link থাকবে।

## Initial dataset scope

Initial district list: চট্টগ্রাম, কক্সবাজার, রাঙ্গামাটি, বান্দরবান, ঢাকা, সিলেট, মৌলভীবাজার, রাজশাহী। প্রথম research pass-এ চট্টগ্রাম ৭৩, কক্সবাজার ৬৯, রাঙ্গামাটি ৪৯ এবং বান্দরবান ৭৪টি deduplicated named visitor destination যোগ করা হয়েছে—beach, lake, riverbank, waterfall, hill/viewpoint, park, museum, heritage/religious, recreation, resort and public attraction category ধরে। ঢাকা, সিলেট, মৌলভীবাজার ও রাজশাহীর initial shortlist পরের pass-এ একই depth-এ expand হবে। Visitor-place datasetটি official district/tourism references, Banglapedia, Forest Department, reputable travel reporting, map-indexed pages ও public listings cross-check থেকে curated করা হয়েছে; এটি exhaustive official gazetteer নয় এবং missing/uncertain coordinates fallback marker হিসেবে ব্যবহার করা হবে। Later districts can be appended without changing the interaction model.

## Design system

- **Design movement:** editorial cartography + warm digital scrapbook.
- **Core principles:** district-first selection, map-first storytelling, one-tap place marking, shareable personal memory.
- **Color philosophy:** river green marks visited geography; paper cream keeps the card archival; coral marks personal memories and selected places; muted grey keeps unvisited districts quiet.
- **Layout paradigm:** asymmetric editorial canvas with a wide district map, compact place list, and poster-like share card.
- **Signature elements:** filled/blank place markers, district boundary map, postal-stamp metadata and selected-place strip.
- **Interaction philosophy:** first choose district, then reveal only its place list; selection is reversible; no account required for the demo flow.
- **Animation:** soft map reveal, marker pulse on selection, hover lift on place rows, short card reveal; motion remains functional and mobile-friendly.
- **Typography:** Anek Bangla for Bengali display/UI and compact uppercase micro-labels for the cartographic/editorial layer.
- **Brand essence:** “আমার জেলা — যে জায়গাগুলো আমি ঘুরেছি।” Personality: rooted, playful, personal.
- **Brand voice:** conversational and memory-led. Example lines: “আগে জেলা বেছে নিন।” and “এই map-এ আমার অনেক গল্প আছে।”
- **Wordmark/mark:** a small rotated map-pin/star mark beside the Bengali wordmark.
- **Signature color:** river green `#0d6b55`.

## Implementation structure

- `client/src/pages/Home.tsx`: tab navigation, district-first selection, place list, map markers/labels, profile fields, preview card, share/export actions.
- `client/src/index.css`: responsive editorial/cartographic visual system, map markers, card layout and print rules.
- `client/public/bd-map.json`: actual Bangladesh district vector geometry.
- `client/public/tourism-spots.json`: initial ৮ district place data, source URLs and approximate coordinates.
- `client/public/manus-routes.json`: public route manifest.
- `server/_core`: existing starter server and health route retained.

## Map behavior

The full district vector map remains visible in a reference-style Bangladesh composition. The chosen district is filled green while other districts remain muted/blank. Each researched place is projected onto the map from its approximate latitude/longitude. Unselected places show as blank dots; selected places show a coral filled dot, halo and Bengali label. The same selected state is reused in the share card.

## Delivery behavior

The current MVP is client-first: visitor place data and vectors are static public assets, user photo stays in-browser, share links encode district and selected places, PNG/JPG export is generated locally, and PDF uses browser print layout. No existing Cloudflare site will be modified. After implementation, code will be pushed to the user’s separate GitHub repository and a new Cloudflare project will be attempted independently.
