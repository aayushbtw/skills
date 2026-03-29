---
name: writing-guide
description: Write, review, and improve articles and blog posts with clear structure, strong voice, and polished prose. Use when the user asks to write an article, draft a post, review writing, or improve existing content.
---

# Writing Guide

## Reviewing

When reviewing existing writing, apply all guidelines below. Focus on the 3 most impactful problems. For each: quote the weak passage, explain why it's weak, and rewrite it. Ask if the user wants you to apply the changes or keep going.

## Voice

Sound like: A senior engineer at a conference afterparty explaining something they're genuinely excited about. Smart, specific, a little irreverent, deeply knowledgeable.

Don't sound like: A corporate blog, a press release, a sales deck, or an AI-generated summary.

- **Talk like a human**: Write the way a sharp engineer talks to peers, not the way a committee writes a memo.
- **Have personality**: Humor should serve the content, not replace it. Sarcasm works. One good joke per post is plenty.
- **Use "we" and "you"**: This is a conversation, not a paper.
- **Be opinionated**: Take a stance. "It depends" is not a conclusion. If there are tradeoffs, say which side you would pick and why.
- **Be honest**: Acknowledge limitations. Readers trust writers who admit what's broken more than writers who pretend everything is perfect.

## Structure

### Titles

The title is the highest-leverage sentence in the post. It must stop someone mid-scroll.

**Strong**: "Your JavaScript bundle has 47% dead code. Here's how to find it."
**Weak**: "Performance improvements in v4.2"

### Opening

The first 2-3 sentences must do one of: state the problem, state the conclusion, or set up a contradiction.

**Good**: "Our cache hit rate dropped to 12% on a Tuesday morning and nobody noticed for six hours. Turns out, the invalidation strategy we trusted for three years had a subtle race condition, and fixing it meant rethinking how we model staleness entirely."

**Bad**: "Caching is an important part of any modern web application. In this article, we will explore some best practices for cache invalidation and share some exciting improvements we've made to our caching layer."

**Contrasting hook**: "When done right, animations make an interface feel faster and more intuitive. But they can also make it feel sluggish and annoying. The difference isn't the animation. It's knowing when not to animate at all."

### Body

Structure around what the reader is wondering, not your internal narrative:

1. **What problem does this solve?** (1-2 paragraphs max)
2. **How does it actually work?** Not buttons-you-click, but underlying mechanics. (Bulk of the post)
3. **What were the tradeoffs?** This separates good from great.
4. **What should I do next?** Concrete next steps.

One idea per section. If you're making two points, that's two sections.

Headings must convey information. "Background" and "Architecture" are useless. "Why pre-aggregation destroys debugging context" tells the reader what they will get.

### Ending

Don't summarize the article back at the reader. Instead, do one of:

- **Extend**: Position the post as an entry point, not the final word.
- **Land a takeaway**: One sharp sentence that reframes what they just learned.
- **Provoke**: A question or challenge that sticks after they close the tab.

## Craft

- **Demonstrate, don't explain**: Ground every principle in something the reader can see, try, or verify.
- **Earn your strong takes**: Show proof first, then state the rule. Bold claims without backing just sound arrogant.
- **First-person specifics**: "I ran this query 200 times a day for a month" beats "many engineers frequently encounter this."
- **Numbers over adjectives**: "Significantly faster" means nothing. "p99 dropped from 340ms to 45ms" means something.
- **Vary the rhythm**: Alternate short punchy sentences with longer ones that build context. A wall of either loses the reader.
- **Cut ruthlessly**: Every sentence must earn its place. Remove filler words (just, really, very, quite, basically, actually, in order to) and redundant qualifiers.
- **Active voice by default**: Passive is fine when the actor is irrelevant or unknown.

## Banned language

If any of these appear in the output, rewrite the sentence.

### Corporate fluff

- "We're excited/thrilled to announce" -- just announce it
- "Best-in-class" / "industry-leading" / "cutting-edge" -- show, don't tell
- "Seamless" / "seamlessly" -- nothing is seamless
- "Empower" / "leverage" / "unlock" -- say what you actually mean
- "Robust" -- describe what makes it robust instead
- "Streamline" -- everyone is streamlining, stop
- "Deep dive" / "game-changer" / "synergy" -- find a fresher way or just say it plainly
- "At [Company], we believe..." -- just state the belief
- "In this blog post, we will explore..." -- just start

### Filler

- Transitions: "That being said," "It's worth noting that," "At the end of the day," "Without further ado," "As you might know"
- Hedges: "It seems like," "I think it's fair to say," "It could be argued that" -- take a position or don't
- Sentence starters: "Importantly," / "Interestingly," / "Notably," -- just say the thing
- Invitations: "Let's dive in" / "Let's explore" / "Let's unpack" -- just start

### AI tells

Dead giveaways that text is AI-generated:

- **Em dashes**: Use commas, periods, or parentheses instead.
- **Smart/curly quotes** (" " ' '): Use straight quotes (" ') only.
- **"You'd" / "you'll" / "they'd"**: These contractions sound robotic. Use "you would" or rephrase. Normal contractions like "don't", "isn't", "we're" are fine.
