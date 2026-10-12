Readme 
Certification Mark Reader
A browser-based scanner that reads BIS, FSSAI and CRS certification numbers from a product label, tells you which mark it found, and checks the number against a database. Show a product to the camera and the app guides you by voice, locks onto the number, and speaks the result.

Note: The database in this project is demo data. The numbers in it are made up and are not linked to any official registry.

Features
Identifies three marks and shows which one was found (BIS, FSSAI or CRS)
A different message for each mark, for example active, expired, or number not found
Live voice guidance that tells you how to move the product (too dark, glare, move left or right, come closer, hold steady)
Photo upload fallback if the camera is unavailable
Accessible design: large button, high-contrast colours, aria-live result regions
Private: images are processed on your device and are never uploaded

Mark	What it is	Number format the app looks for
BIS	Bureau of Indian Standards licence	CM/L- followed by a number, e.g. CM/L-1234567
CRS	BIS Compulsory Registration Scheme	R- followed by 8 digits, e.g. R-41005678
FSSAI	Food Safety and Standards Authority of India licence	A 14-digit number, e.g. 12345678901234
The mark is identified from the format of the number, not from the logo image.

How it works
Camera frame
    |
    +--> Scout (every frame, a few ms)
    |      Finds text-like shapes, drives voice guidance,
    |      and notices when the product moves away
    |
    +--> Reader (back-to-back OCR with Tesseract.js)
           Enhances the frame, reads text, matches the
           BIS / CRS / FSSAI patterns
                |
                v
          Lock on number (confidence >= 55%)
                |
                v
          Zoom crop (up to 4x) + second OCR read
          with a digits-and-letters whitelist
                |
                v
          Database check (mark + number must both match)
                |
                v
          Show result + speak it once, then go silent
States
The scanner is always in one of four states: idle, scanning, verifying or frozen. A runId counter cancels any older work when you press Rescan, so a stale result can never appear.


