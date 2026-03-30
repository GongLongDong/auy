# Word-Formation as Program Execution (Core Rules)

> **Chinese version**: **`rule.md`** (maintain in sync with this file).  
> **Purpose**: Analyze how **letter sequences in English (and analogous languages) execute like a program**—the **core idea** for morphological analysis.  
> **Relation**: Works **alongside** **`RULES_YIYIN.md`** (master rule card, glossed examples); on conflict, **your later revision wins**.  
> **Notation**: **No subscripts on letters** (no `a₀`, `e₁`); when the **same letter** appears more than once, disambiguate **in prose** (e.g. “initial `a`”, “per-stage `a`”, “previous-step `e`”).

---

## 1. Overview

- **Consonants** behave like **functions**, **called left to right**.  
- **Vowel `a`**: often a **parameter** (total amount, step size, stage amount—**role depends on the word**).  
- **Vowel `e`**: **intermediate value / current amount**—the **`e`** **produced** by the previous step is passed onward; **when present it must be the first argument** (see §2).  
- **Unfamiliar words**: **try parsing them with this file first**; entries **not yet in the docs** may be labeled **tentative**, and **historical etymology** should be kept on a **separate track** (etymology does **not** by itself falsify this model).

---

## 2. Argument Order (Hard Rule)

- **Multiple arguments**: the **result from the previous step** (usually **`e`**) **always comes first** (when it exists).  
- **`van(e, a)`**: **neither may be omitted** (when both apply). **`e` first**, **`a` second**.  
- **General rule**: **whenever a prior step yields a value, the next function lists that value first among its arguments.**

---

## 3. Fixed Combinators (“one function body”)

- **`ct`**: **`c` and `t` in one step**, **not two separate calls** (read together in analyses like **`fact`**).  
- **`ce`**: **`c` plus `e`** as a **lock / closure** bundle on the letter tier (read with **`advance`**, etc.).  
- **`cin`**: **`c` + `i` + `n`** as **one callable block**, shape **`cin(e, i)`** (common on progressive chains; **do not** rename the block as a bare **`c(8, i)`**).

---

## 4. Basic Examples

### 4.1 `act`

**`c(a) → e → t(e)`**

- **`c`** takes argument **`a`**, **finishes**, emits one **`e`**.  
- **`t`** then uses that **`e`** for **state / closure**.

### 4.2 `fact`

- **Fine-grained**: **`f(a) → e → c(e) → e → t(e)`**  
- **With merged `ct`**: **`f(a) → e → ct(e) → e`**  
- **`f` runs first**, then either **`c` … `t`** or **`ct`**; **both notations coexist**—pick by desired granularity.

---

## 5. `pen`, `en`, and `ped`

### 5.1 `pen` (pen / writing loop unit)

- **Loop spine**: **call `p` → get `e` → enter `n` with that `e` → back to `p`** (**`p → e → n(with e) → back to p`**).  
- **`n`**: **loop head**, like **entering a `for`** in code.  
- **Two states**: **not writing** = the **`pen` machine is idle**; **start writing** = **enter the loop, it runs**.  
- **`pen`** can be treated as a **loop unit pluggable into a larger continuous sequence** (ongoing writing).

### 5.2 `en`

- **Still ongoing**: **keeps cycling**.  
- **Stopped**: **loop halts**, **frozen at the current step** (idle at that value).

### 5.3 `ped` and progressive aspect

- **While the action is still running**: when the **last step lands on `d`**, **`d` keeps running and does not hand back a final result** (**no `return`**).  
- **Shared with `pen`**: **progressive ⇒ tail step often does not finalize**; **difference**: on the **`n` side** you **loop back to `p`**; on the **`d` side** you **head toward closure but progressive aspect leaves it suspended**.

---

## 6. `penden` (thought-experiment word)

- **Macro-cycle** (example: **run two rounds**): run **`pen` once** → **`e` produced by `n` is not spelled**; **`d` follows `n` directly**—**`n`’s output feeds `d`** → run **`den` once** → **return to the start**, **repeat**.  
- **Spelling alignment**: **p e n d e n**; the **`e` after `n` inside `pen` is not written**—**`n` is immediately followed by `d`**; the **`e` inside `den`** is the next explicit **`e`**.

---

## 7. Loop Count

- **Fixed count** (e.g. **100**): the **whole-word macro-loop runs 100 times**.  
- **Treated as still in progress**: **unbounded iterations**, **keep looping** until **something external stops it**.

---

## 8. `advance` / `advancing`

### 8.1 Chunks

- **`advance`**: **`ad` + `van` + `ce`** (letters **a-d | v-a-n | c-e**).  
- **`advancing`**: **a d v a n c i n g** — **no stem-final `e`**, **`ing` attached**; **`ad` + `van` + `c` + `ing`**.  
- **Two `n`’s**: the **first** sits in **`van`** (**intra-stage loop**); the **second** sits in **`ing`** (**outer “progressive” ring**)—they can **stack as inner + outer** loops.

### 8.2 Short form (non-progressive skeleton)

**`d(a) → van(e, a) → ce(e) → e`**

- **`d(a)`**: **obtain total / current amount** (e.g. “10 to cover” or an **abstract goal slot**).  
- **`van(e, a)`**: **`e` from the previous step**; **`a` in this pattern can be step size** (e.g. **2 meters**); for **abstract motion** (goal Paris), **`e` can stand for “the slot that is the destination”**, **segment length need not be fixed up front**, and **`van` still advances one bite per lap**.

### 8.3 `advancing`: programmatic loop (numeric + abstract)

**Concrete walk** (**10 meters** forward, **2 meters** per step):

1. **`d(a)`** → **yields 10**.  
2. **`van(e, a)`** → **`van(10, 2)`**: after one step **8** remains; **here the second argument `a` = step 2 m**.  
3. **`cin(e, i)`** → **`cin(8, i)`**: **`c` read as /s/ ≈ `set`**, **passes the current value (8) onward** (**hold / relay**—tighten per word as needed).  
4. **`g(e) → g(8)`**: **like global storage**, **still 8**; **next round from the outermost loop head back to `van`** → **`van(8, 2)`**, **and so on**.

**Abstract motion** (Paris as goal): **“10” can be read as “the Paris goal slot”**; **`van` still moves one segment per lap**, **segment size can stay unspecified at the start**.

### 8.4 Grammar and tense / aspect

- **`advance` → `advancing`**: in this model, morphology adds **`ing` (and `cin`, `g`, etc.)** on the chain—**compatible with progressive and related categories**; **other tenses / aspects** can be read as **the same skeleton with different outer wrappers or different “final return” behavior**.

---

## 9. Phonology Notes (readable with letter-`e` sense)

- **`/e/` and `/ei/`**: in your system they **align for conditioning** (read with **`RULES_YIYIN.md` §4.2, `ɛ` = `ei`**).  
- **Vowel e vs vowel i**: **e** skews **stepwise / cyclic** change; **i** skews **one continuous line to the endpoint** (read with **`e.md`**, **`/iː/`**).  
- **Letter-tier `e`**: **changing “amount left to close”**, **dual focus with `a`**—see **`e.md`**.

---

## 10. Cross-References

- **Master card and glossed examples**: **`RULES_YIYIN.md`** (e.g. **`advance` §6.23**, **`act` §6.7**).  
- **Letter `e` canon**: **`e.md`**.  
- **Maintenance**: by default **discussion-only, no file edits**; when you say **「更新」 / “update”**, revise **`RULES_YIYIN.md`**, **`rule.md`**, and **`rule_en.md`** **in sync**.

---

*Drafted from user sign-offs in session; extend incrementally as study deepens.*
