# Landed — your website (no coding needed)

## The files
| File | What it is |
|---|---|
| `index.html` | Your whole website. All your numbers live in the **CONFIG** block at the top. |
| `api/quote.js` | Reads product pages automatically (title, price, photo). |
| `api/track.js` | Powers "Track order" — reads your Google Sheet. |

---

## 1. Put it online (about 10 minutes)

1. Go to **github.com** -> sign up free.
2. Click **+** (top right) -> **New repository** -> name it `landed-site` -> **Create**.
3. Click **"uploading an existing file"** -> drag in `index.html`, `README.md`
   **and the `api` folder** -> **Commit changes**.
4. Go to **vercel.com** -> sign up -> **Continue with GitHub**.
5. **Add New -> Project** -> find `landed-site` -> **Import** -> **Deploy**.

You now have a live site like `landed-site.vercel.app`.

---

## 2. Fill in your details

Open `index.html` on GitHub, click the **pencil** icon, edit the CONFIG block,
then **Commit changes**. Vercel republishes in about a minute.

```
officialRate: 1360      <- today's official NGN per $1. Update this regularly.
buffer: 15              <- your spread. Customers see 1360 + 15 = 1375
serviceFeePct: 4        <- your service fee
dutiesPct: 5            <- customs & duties estimate
shipPerKgUSD: 12        <- what you charge per kg to Nigeria
delivery: [...]         <- your four delivery prices
whatsappNumber          <- your WhatsApp Business number, e.g. "2348012345678"
paystackPublicKey       <- from Paystack dashboard, starts with pk_
```

---

## 3. Switch on payments

Paystack -> Settings -> API Keys -> copy the **Public key** (`pk_live_...`)
-> paste into CONFIG where it says `pk_test_REPLACE_ME`.

> Live payments need approved CAC registration. Start that early.

---

## 4. Switch on automatic price reading (optional but worth it)

1. Sign up at **scraperapi.com** (free trial credits, then from ~$49/month).
2. Vercel -> your project -> **Settings -> Environment Variables**:
   - Name `SCRAPER_API_KEY`, Value = your key -> **Save** -> **Redeploy**.

Without it the site simply asks the customer to type the price. Nothing breaks.

---

## 5. Switch on order tracking

1. New Google Sheet. Row 1 headers exactly:
   `ref | stage | summary | eta | note`
2. One row per order, e.g.
   `LND-K3M9P2 | 3 | 2 items, 1.5kg | 12 Aug | Weighed 1.3kg - refund sent`
   **stage** is a number:
   `0` placed, `1` bought, `2` heading to US warehouse, `3` at warehouse,
   `4` flying to Nigeria, `5` customs, `6` in Nigeria, `7` ready for you, `8` delivered
3. **File -> Share -> Publish to web -> Entire document -> CSV -> Publish**, copy the link.
4. Vercel -> **Settings -> Environment Variables** -> `SHEET_CSV_URL` = that link
   -> **Redeploy**.

Now you change a number in the sheet and the customer's tracking page updates.

---

## Before you take real money
- [ ] WhatsApp number in CONFIG
- [ ] Today's exchange rate in CONFIG
- [ ] Paystack live public key in CONFIG
- [ ] Send yourself a test order end to end
- [ ] Confirm your US forwarder's real per-kg rate matches `shipPerKgUSD`

## Ongoing costs
- Vercel - free at your scale
- ScraperAPI - from ~$49/month (only if you turn on auto price reading)
- Paystack - about 1.5% + NGN 100 per transaction, capped
