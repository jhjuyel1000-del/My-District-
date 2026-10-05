# আমার এলাকা — Implementation Plan

## Product direction

“আমার এলাকা” একটি বাংলা-first interactive social-card maker। User শুরুতেই দুটি mode পাবে: **আমার এলাকা** এবং **আমার সম্পর্কে**। Mode বদলালে question set, result title, stats, phrase এবং card narrative বদলাবে। Background visual হিসেবে বাংলাদেশের ৬৪ জেলার public vector map ব্যবহার হবে। User জেলা বেছে নিয়ে নিজের নাম/ছবি/উত্তর দিয়ে animated map-card তৈরি করবে এবং PNG/JPG/PDF/share link পাবে।

## Design system

- **Design movement:** editorial cartography + warm digital scrapbook.
- **Core principles:** map-first storytelling, playful self-expression, fast mobile creation, shareable reveal.
- **Color philosophy:** deep river green anchors trust and place; coral marks personality; warm paper and mango yellow create memory and human warmth.
- **Layout paradigm:** asymmetric editorial canvas; large map shapes and floating photo cards instead of a generic centered dashboard.
- **Signature elements:** district boundary/map outline, postal-stamp style card metadata, landmark dots and dotted-route motifs.
- **Interaction philosophy:** one-tap selection, short funny questions, progressive reveal, visible privacy choice, no forced account for the demo flow.
- **Animation:** map/landmark reveal, soft hover lift, progress transitions and result-card reveal; motion stays short and functional.
- **Typography:** Anek Bangla for Bengali display and UI hierarchy, with spacious uppercase micro-labels for the cartographic/editorial layer.
- **Brand essence:** “Your map, your story”—for people who want to turn hometown identity or personality into a social object. Personality: warm, witty, rooted.
- **Brand voice:** conversational, teasing, locally aware. Example lines: “আপনার map-এ আপনার গল্প।” and “একটু বসি—কিন্তু উঠি কালকে।”
- **Wordmark/mark:** a rotated map-pin/flower star mark beside the Bengali wordmark.
- **Signature color:** river green `#0d6b55`.

## Implementation structure

- `client/src/pages/Home.tsx`: homepage, mode selection, 64-district picker, mode-specific questions, image upload, result card, share/download actions.
- `client/src/index.css`: responsive editorial/cartographic visual system and print rules.
- `client/public/bd-map.json`: district vector geometry used by the interactive map card.
- `client/public/manus-routes.json`: public route manifest.
- `server/_core`: existing starter server and health route retained.

## Map source/licensing decision

The site uses the project’s existing district vector asset for the 64 districts and keeps public geographic attribution in the footer. A production release should replace/confirm the asset’s exact upstream license and add a dedicated attribution page before commercial publication. No copyrighted third-party artwork is copied into the card design.

## Delivery behavior

The current MVP is client-first: card preview is instant, user photo stays in-browser, share links encode the selected mode and district, PNG/JPG export is generated locally, and PDF uses the browser print layout. Public gallery, persistent accounts and server-side card storage remain planned follow-up capabilities.
