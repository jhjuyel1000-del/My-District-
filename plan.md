# বাংলাদেশ ভ্রমণ ম্যাপ — Implementation Plan

## Product scope
রেফারেন্সের মতো বাংলা, এক-পেজের ইন্টার‌্যাক্টিভ ভ্রমণ ম্যাপ: আমার ম্যাপ, বিশ্ব ম্যাপ, কোথায় ঘুরবেন, খেলা এবং ট্রিপ প্ল্যানার—সব সেকশন একই নেভিগেশন ও ভিজ্যুয়াল ভাষায় থাকবে। ব্যবহারকারী জেলা/দেশ নির্বাচন, থিম বদল, নাম ও ছবি যোগ, ম্যাপ রেন্ডার এবং PNG/JPG/PDF এক্সপোর্ট করতে পারবেন।

## Design direction
- **Design movement:** editorial travel journal + soft neo-brutalist card UI; অফ-হোয়াইট কাগজ, ink-green, coral, mustard accent।
- **Core principles:** (১) মানচিত্র আগে, (২) বাংলা কনটেন্টে স্বচ্ছতা, (৩) tactile chip/button interaction, (৪) ছোট স্ক্রিনেও এক-হাতে ব্যবহারযোগ্য।
- **Color philosophy:** বাংলাদেশের সবুজ ও নদীর নীলকে base করা, coral/mustard দিয়ে action এবং selection highlight করা।
- **Layout paradigm:** hero-led vertical journey; দুই-কলামের builder zone এবং section-based scroll navigation, জেনেরিক centered dashboard নয়।
- **Signature elements:** dotted border, গোলাকার route-marker, offset shadow cards, map-grid overlays।
- **Interaction:** selection-এ immediate visual feedback, section anchors, live counters, modal guide, quiz/puzzle score feedback।
- **Animation:** hero fade/float, card hover lift, map pulse, selection pop; prefers-reduced-motion সম্মান করা।
- **Typography:** Google Noto Sans Bengali / system sans; বড় condensed-style বাংলা headline, readable 16–18px body।
- **Brand essence:** “নিজের ভ্রমণকে মানচিত্রে রেখে দেওয়ার বাংলা travel scrapbook”—ব্যক্তিগত, খেলাধুলাপূর্ণ, আবিষ্কারী।
- **Voice:** “মানচিত্রে টিক দিন, স্মৃতিগুলো সাজিয়ে নিন।” / “আজ কোন জেলায় যাবেন?”
- **Wordmark:** compass-pin glyph + “পথের খাতা” wordmark। Signature color: #0f7a5c।

## Project structure
- `client/src/App.tsx`: single-page app state, section navigation, selection, exports, quiz/puzzle and planner interactions.
- `client/src/index.css`: responsive visual system, hero/map/card layout, animation and print styles.
- `client/public/manus-routes.json`: `/` route declaration for WebDev.
- `server/_core/index.ts`: existing health endpoint and Vite/production serving; no new API needed for local-first browser state.
