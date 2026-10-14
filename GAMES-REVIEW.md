# Games Review & Fix Plan

Bo-Kata aur Load-Shedding ko chhor kar baqi games ka review, aur har ek ko mazedaar banane ka plan.
Jab agla game theek karna ho to is file ka reference do.

## Status

| Game | Status |
|---|---|
| Lantern Drift | ✅ Dobara likh diya (Ravi par diye, lau, combo, bhanwar) |
| Maze Quest | ✅ Dobara likh diya (andheri galiyan, torch, Moti kutta, chabi + darwaza, levels) |
| Moonlight Moth | ⏳ Baqi |
| Paper Skies | ⏳ Baqi |

---

## Bo-Kata kyun maza deta hai (yehi standard hai)

1. **Ek asli mechanic jis mein skill lagti hai.** Dor ki physics, pench, jitna tez hilao utna tez katta hai. Pench meter tension banata hai.
2. **Muqabla.** AI patangein khud aap ki dor ka peecha karti hain.
3. **Har lamhe ka feedback.** Rub ki awaaz, sparks, "Bo Kata!" ka nara Urdu mein, girti hui patang.
4. **Seedha khel.** Koi start button nahi, aasman pehle se basa hua, game kabhi khatam nahi hota.
5. **Pehchaan.** Basant, Lahore ki chhatein, "kaati/katwayi".

Copilot wale charon games ek hi template the: start panel, timer, lives, "X collect karo, Y se bacho". Sirf bugs theek karne se ye Bo-Kata jaise nahi banenge. Har ek ko **ek asli mechanic + desi rang + juice (awaaz, nare, screen shake)** chahiye.

### Har game mein ye cheezen honi chahiye
- Start overlay nahi. Pehli tap/drag par khel shuru, game over par tap karo to dobara shuru.
- Pehle frame se scene bhara hua ho (Bo-Kata ki tarah 60-90 frames pehle se simulate karo).
- Sound pehli tap par shuru ho (Web Audio), mute button ho.
- Combo/streak aur Urdu nare (`Shabash! شاباش`, `Wah wah! واہ واہ`, `Kamaal! کمال`).
- Fonts: Rozha One + Noto Nastaliq Urdu + IBM Plex Mono (Bo-Kata wala HUD style).
- Physics frame-rate independent ho (`Math.pow(damp, dt)` ya spring `ax = (t-x)*k - v*c`).
- `localStorage` ko hamesha `try/catch` mein wrap karo.
- Touch par object ungli se thora ooper rakho taake ungli ke neeche na chhupe.

---

## Lantern Drift ✅ (ho gaya)

**Purane masle:**
- Kashti ~28 px/s par atak jati thi. Damping har frame lagti thi, is liye 120Hz par aur bhi dheemi.
- Arrow keys toot chuki thin, target `0 ± 1` tha, kashti kone ki taraf bhagti thi.
- 50% lanterns screen ke bahar paida hoti thin aur wahin rehti thin.
- `sound.collect()` / `hit()` kabhi call nahi hote the, awaaz hi nahi thi.
- Badal start par hi kashti ke upar aa sakte the.

**Naya design:** Raat ka Ravi, kaghaz ki kashti mein diya. Lau kam hoti hai aur andhera qareeb aata hai. Darya ke diye uthao to lau barhe. Combo par sur ooper jata hai. Bhanwar kheenchta hai (gird diyon ka chakkar, risk aur inaam). Chattanon ke beech tang rasta, tirchi lakdi. Takkar par lau kam, combo khatam, screen shake.

**Baqi kaam:** Test mein bina kuch kiye kashti 30-70s zinda reh jati hai. Khel kar dekho, zarurat ho to `flame -= (5 + d * 4) * dt` aur diya ka `+8` tune karo.

---

## Maze Quest ✅ (ho gaya)

**Bugs** ([maze-quest/index.html](maze-quest/index.html)):
- **Har baar wahi maze.** `carve()` (line ~183-194) directions shuffle nahi karta. Fix: `dirs` ko Fisher-Yates se shuffle karo.
- **Deewaron mein aadha ghar ghus jate hain.** Logic `floor(player.x)` se cell leti hai, lekin drawing `x*cell + cell/2` par hoti hai. Fix: grid-snapped movement (cell se cell tween) ya `floor(x + 0.5)`.
- **Intro panel kabhi nazar nahi aata.** Load par hi `startGame()` chal jata hai aur timer shuru ho jata hai.
- **Mobile par khel nahi sakte.** Touch/swipe controls hain hi nahi.
- **Jeetne ka message toota hai.** `textContent` mein `<b>` tags (line ~262, 311) seedhe text ban kar dikhte hain.
- Diagonal input par deewar se phisalne ki bajaye ruk jata hai.
- HUD par gems ka "x/7" nahi dikhta.
- `resize()` mein `W * devicePixelRatio || 1` operator precedence ghalat hai, aur DPR clamp canvas size par lagu nahi hota.

**Naya design: "Andaroon Lahore ki galiyan"**
- Torch jitni roshni, baqi andhera (Load-Shedding wala darkness mask).
- Ek peecha karne wala kirdar, jaise mohalle ka kutta jo awaaz par aata hai. Bhaagne ka tension.
- Har baar naya maze, levels ke saath bara hota jaye.
- Grid-snapped smooth movement aur swipe controls.
- Collectibles desi hon (jalebi, samosa, chabi), aur darwaza khulne par nara.

---

## Moonlight Moth ⏳

**Masle** ([moonlight-moth/index.html](moonlight-moth/index.html)), bugs kam hain lekin challenge zero:
- **Seeds kabhi ghaib nahi hote.** Har ~0.85s mein naya aata hai, screen bhar jati hai aur glow hamesha full rehta hai.
- **Shadows bohat dheeme hain** (20-46 px/s). Mushkil kabhi nahi barhti.
- **Haarne ke teen raste hain** (time, glow, wings). Confusion hoti hai, tension nahi.
- Koi awaaz nahi.

**Naya design: "Parwana aur shama"**
- Beech mein shama. Jitna qareeb jao, points utne tez (multiplier).
- Zyada qareeb jao to par jalne lagte hain (heat meter). Risk aur reward ka khel.
- Hawa ke jhonke shama ki lau ko hilate hain, safe zone badalta rehta hai.
- Sirf ek fail state: par jal gaye ya andhera ho gaya.
- Doosre parwane bhi aate hain jo jagah ke liye takrate hain.

---

## Paper Skies ⏳

**Masle** ([paper-skies/index.html](paper-skies/index.html)):
- **Ring miss karo to life chali jati hai.** Rings har ~1.6s mein aati hain, bohat sakht hai.
- **Kuch rings ka miss hona tay hai.** Rings aur badal alag alag spawn hote hain, aksar badal bilkul ring ke saamne aa jata hai.
- **Mouse-follow bohat aasan hai.** Plane cursor ke peeche khud chalta hai, koi skill nahi lagti.
- Ring face-on gol dikhti hai, plane us mein se "guzarta" mehsoos nahi hota.
- Koi awaaz nahi.

**Naya design:**
- Glide physics: dabao to dive (speed barhe), chhoro to upar uthe lekin speed kam ho. Speed hi score multiplier ho.
- Ring combo/streak. Miss par sirf combo toote, life nahi.
- Rings aur badal mil kar designed patterns mein aayein (taake har miss player ki ghalti ho).
- Ring ellipse ho, pichla hissa plane ke peeche aur agla aage draw ho, taake guzarne ka ehsaas ho.
- Desi rang: Basant ka din, chhaton ke ooper, ya Margalla ki pahariyan.
