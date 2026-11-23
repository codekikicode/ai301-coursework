I found a bug that made a climate model silently ignore users' configuration
changes, and I opened a fix as a pull request to the Community Terrestrial
Systems Model (CTSM): https://github.com/ESCOMP/CTSM/pull/4344

When the same setting was given to the model in two places at once, its build
tool quietly picked one and never told the user — so people ran long
simulations believing they'd changed something they hadn't. I proved the
behavior with a reproduction, added a check that stops the build with a clear
error naming the conflict, and wrote an automated test that fails without my
fix and passes with it. The pull request is open with passing checks.

The part that changed how I work wasn't the code: a grading tool caught me
arguing from an assumption I hadn't verified, and deleting that argument — not
the patch — was what made the plan hold up. Rigorous tests can also lie in
subtle ways, and learning to distrust a green run until I knew *why* it was
green was worth the whole week.

#OpenSource #SoftwareTesting