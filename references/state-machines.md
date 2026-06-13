# Mechanism as State Machine — Prove the Logic, Don't Just Animate It

Rule 17. The references *animate* mechanisms; we **prove** them. Many mechanisms (a
click pen, an escapement, a latch, a gearbox shifter, a UI flow) are state machines.
Model the states + transitions as data, render the figure from the current state, and
show a **linked state diagram** (rule 16) so the reader sees *why* it behaves as it does.
Demonstrated in `../assets/examples/state-machine.html` (the click pen).

## Why this beats animation

An animation shows *that* it moves. A state machine shows *why*: which inputs are legal
in each state, what each transition changes, and which invariants hold. The click pen's
"aha" — the cam rotates the **same direction** on every release, yet the tip alternates
because the *seats* alternate — is invisible in a pure animation and obvious once you
step the machine. Proof, not assertion.

## The pattern

1. **Model transitions as data.** A map of `state → { event → nextState }`. This is the
   single source of truth; everything else derives from it.

   ```js
   const MACHINE = {
     S0:{ name:'Retracted', next:{ push:'S1' } },
     S1:{ name:'Depressed', next:{ release:'S2' } },
     S2:{ name:'Extended',  next:{ push:'S3' } },
     S3:{ name:'Depressed', next:{ release:'S0' } },
   };
   ```

2. **Keep a tiny live state + derived physics.** The current state id plus any counters
   the physics needs. Derive physical quantities (positions, angles, flags) from them —
   never store what you can derive.

   ```js
   const state = { s:'S0', releases:0, lastEdge:null };
   const tipOut  = state.releases % 2 === 1;     // derived
   const camDeg  = state.releases * 45;          // monotonic — the honest mechanism
   ```

3. **One `step(event)`** that consults the table, refuses illegal events, records the
   edge taken, and re-renders. Illegal inputs simply do nothing — that *is* the logic.

4. **Render the figure from state**, easing moving parts via CSS transitions (plunger,
   tip, cam rotation). Same state → same picture, deterministic.

5. **Link a state diagram.** Draw nodes + directed, labelled edges; on each render
   highlight the **current node** and the **last transition edge** (accent). The reader
   watches the abstract machine and the concrete mechanism move together (rule 16).

6. **Expose the events as controls, not a timeline.** A button per legal event (label it
   with the available event), plus a convenience "do a whole cycle" button. Stepping
   one event at a time is what makes the logic legible; keep that the primary affordance.

## Doing it honestly (rule 15)

- **Monotonic truth.** If the real cam only ever rotates one way, model that (a
  release counter), and let the alternation fall out of geometry — don't fake a
  back-and-forth. The honest model is what teaches.
- **Name transient vs. stable states.** Depressed-held states (S1, S3) are real and
  distinct from resting states (S0, S2); showing them prevents the "magic toggle" feel.
- **Surface invariants** in a readout ("notch 3 · shallow", "tip OUT") so the reader can
  check the claim against the picture.

## Where this generalises

- **Escapement:** locked → impulse → released → locked; the diagram proves it advances
  one tooth per oscillation.
- **Latches / locks / relays:** legal vs. illegal transitions are the whole point.
- **UI / protocol flows:** the same pattern documents a checkout flow or a handshake —
  the figure becomes living documentation that *proves* reachability and dead-ends.

## Checklist

- [ ] Transitions are data; the figure derives from `state`, stores nothing derivable?
- [ ] Illegal events are no-ops (the machine enforces its own rules)?
- [ ] A linked state diagram highlights current node + last edge each render? (rule 16)
- [ ] Stepping one event at a time is the primary control (not a scrubbed timeline)?
- [ ] The honest invariant is modelled (e.g. monotonic rotation) and shown in a readout? (rule 15)
- [ ] Deterministic + dark/light + reduced-motion safe (CSS-eased, no autoplay required)?
