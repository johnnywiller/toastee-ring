# Toastee Ring 🎤

A hand-drawn, interactive web page for [Toastmasters](https://www.toastmasters.org/) clubs.  
Members stand in a visual circle holding hands — experienced speakers are always placed next to newer ones, so anyone with a question knows exactly who to turn to.


## What it does

- Draws all club members as sketchy stick figures in a circle
- Each figure has an emoji face, a name, and a level badge
- Higher-level members are automatically placed next to lower-level ones (see [The Algorithm](#the-algorithm))
- Add or remove members on the fly — the ring reshuffles instantly
- Emojis and colours are remembered per person across page reloads
- Fully static — works on GitHub Pages with no backend

## Members file

Edit `members.toml` to manage your club roster:

```toml
[[members]]
name = "Alice Smith"
level = 5

[[members]]
name = "Bob Jones"
level = 1
```

Levels go from **1** (newcomer) to **10** (distinguished). The page reloads the file on every visit, so keeping the TOML up to date is all you need to do.

## The Algorithm

The goal: every experienced member holds hands with newer ones on both sides.

1. **Sort** members by level (highest first)
2. **Split** into a high half and a low half
3. **Interleave** them — high-level members fill the even slots, low-level fill the odd slots

```
Sorted:     Maria lv5 · Janine lv4 · Marie-Pierre lv3 · Nabeelah lv2 · Johnny lv1

High half:  Maria lv5 · Janine lv4 · Marie-Pierre lv3
Low half:   Nabeelah lv2 · Johnny lv1

Ring order: Maria lv5 → Nabeelah lv2 → Janine lv4 → Johnny lv1 → Marie-Pierre lv3 → (back to Maria)
```

Every senior member ends up flanked by junior ones.
