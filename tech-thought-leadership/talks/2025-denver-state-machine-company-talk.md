# Your Company Is A Git Repository: Running Your Startup as a State Machine

**Event:** Denver Startup Week / Colorado AI Summit
**Date:** Wednesday, September 17, 2025  
**Time:** 11:00am - 12:00pm MDT  
**Location:** TBD
**Speaker:** Chris McDermut

---

## Talk Abstract

What if your entire company could run from a Git repository? Not just your code—your roadmap, your decisions, your team, even your "employees." 

In this mind-bending talk, I'll show how I run my startup using Git as the operating system, with billionaire-themed worktrees as my workforce. Meet Bezos (my backend engineer), Musk (my frontend dev), and Gates (my QA engineer)—all managed through a tool called Proletariat that makes parallel AI development actually fun.

This isn't theory. I'll demonstrate live how I ship features faster than teams 10x my size, using Git commits as company state transitions, markdown specs as executable strategy, and AI agents that read my repo to understand their jobs. 

You'll leave knowing how to turn your chaotic startup into a deterministic state machine that can be run by humans today and AI agents tomorrow.

---

## Hook Options (Choose One)

### Option A: The Billionaire Angle
"I Hired Jeff Bezos, Elon Musk, and Bill Gates to Build My Startup (They're Git Worktrees)"

### Option B: The Philosophical Angle  
"Your Company Is Already A State Machine—You Just Don't Know It Yet"

### Option C: The Practical Angle
"How I Ship 10x Faster Using Git As My Company OS"

---

## Key Takeaways

1. **The State Machine Mental Model**: Why companies are just repositories with commits
2. **Practical Implementation**: Turn your repo into your company OS today
3. **The Billionaire Workforce**: Using themed worktrees for parallel development
4. **AI-Ready Architecture**: Build companies that agents can run
5. **Live Demo**: Watch me hire Bezos and ship a feature in real-time

---

## Talk Outline

### 1. The Aha Moment (5 min)
- "I realized my company IS my Git repository"
- Everything is state: code, docs, roadmap, decisions
- Commits are state transitions
- Show actual repo structure

### 2. The State Machine Company Pattern (10 min)
```
/your-company
├── /apps           (products)
├── /pmo            (project management)
│   ├── kanban.md   (current state)
│   └── /specs      (strategy as code)
├── /context        (company knowledge)
└── /packages       (shared resources)
```
- Live tour of CareerOps repo
- Show how specs become features
- Demonstrate kanban as state tracking

### 3. Enter The Billionaires (10 min)
- "But I needed parallel development..."
- Demo: `prlt hire bezos musk gates`
- Each billionaire works on different features
- Show actual worktree structure
- The psychology of themed development

### 4. Live Demo: Shipping With Billionaires (15 min)
```bash
# Live on stage
$ prlt hire bezos --task="add-analytics"
💰 BEZOS: Ready to work!

$ cd ../careerops-staff/bezos
$ git checkout -b analytics-feature
$ # Actually build feature
$ git commit -m "feat: add Posthog analytics"

$ prlt status
💰 BEZOS: ✅ Feature complete
💰 MUSK: 🔨 Working on Chrome extension
💰 GATES: 🧪 Writing tests
```

### 5. The AI Future (10 min)
- "What if Bezos was an actual AI agent?"
- Show concept: `prlt hire bezos --ai`
- AI reads specs, writes code, opens PRs
- Company runs itself
- You just manage the state machine

### 6. How To Start Tomorrow (5 min)
- Template repo structure
- Install Proletariat
- Write your first spec
- Make your first state transition
- Join the movement

### 7. Q&A (10 min)
- "Is this insane?" (Maybe, but it works)
- "Does this scale?" (I'll tell you at 100 employees)
- "Can I hire Zuckerberg?" (Yes, any billionaire works)

---

## Memorable Quotes

- "Your company is just a Git repository that makes money"
- "I commit, therefore I am... profitable"
- "Bezos works weekends because he's just a worktree"
- "The best employees are the ones you can `git reset --hard`"
- "We're all just state machines pretending to have free will"

---

## Demo Requirements

- [ ] Laptop with Proletariat installed
- [ ] CareerOps repo ready
- [ ] Pre-created worktrees for safety
- [ ] Backup slides if demo fails
- [ ] Test conference WiFi/projection

---

## Why This Talk Matters

**For Founders**: A new way to think about company operations
**For Developers**: Make parallel development fun again
**For The Future**: AI agents need structured environments to operate

This isn't just about Git or development tools. It's about reimagining what a company is in the age of AI.

---

## Social Media Angle

**Pre-talk buzz**:
- "I'm giving a talk about hiring billionaires to build my startup"
- Screenshot of `prlt hire bezos musk`
- "Your company is a state machine" memes

**Post-talk**:
- Open source the template
- Share recordings
- Build community around #StateMachineStartup

---

## Contact

- GitHub: [Proletariat repo]
- Website: proletariat.dev (if you build it)
- CareerOps: Proof it works

---

*Note: This talk is designed to be memorable, practical, and slightly mind-blowing. It positions you as a thought leader while actually helping people ship faster.*