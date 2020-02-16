# Unit Testing

SDLC: software development life cycle

Two different methodologies for unit testing/SDLC:

*Waterfall:*
- needs
- budget/time
- requirements/features
- coding
- UAT: user acceptance testing
  - makes sure everything works as intended
  - it's easy to get stuck in a coding/testing loop and delay release, which can cause a company to fail (waterfall is not recommended for startups because of this)
- deployment
- *revision maintenance
- more controlled procedure; repeat the cycle from top down every time
- it can take years to release another version

*Agile:*
- triangle of budget time, needs and coding
  - pretty important; ~6 weeks
  - coding each individual component and feature as you go along
    - typically, in versions, you release one or so features at a time
- within that triangle, we determine the features
- agile is a contentious issue:
  - some people don't think it requires a planning/needs step
  - in each version, another feature is added/removed
- not very popular, but it is probably better for small companies/startups
- you kind of just wing it as you go
- you can get individual features out quickly

## Testing: Who, When, How, Why... Why

In the waterfall model (easier to talk about here), with coding, you're coding, testing, coding, testing, coding, testing, etc... UAT is user-focused, so if you're in the coding cycle, you might not know how your piece interacts with the larger picture. There is a large gap between the coding cycle and UAT. That's where QA/QC comes into play.

Manual testing overview:
- Does it work?
- What if I did this, option A?
- What if I did this, option B?

Manual testing pros and cons:
- time consuming
- unreliable
- not very repeatable
- flexible (good!)
- exploratory (good!)

Manual testing is not reliable. It's only as good as your attention span, and it's not very repeatable. It's very time consuming. However, it is flexible and explanatory. You're looking in different places in the system and seeing how they interact with the user.

Automated testing pros and cons:
- fast
- reliable
- repeatable
- rigid (bad)
- focused (bad)

Unit testing: Define the condition, the expected result, and assert the real world effects for an individual piece of code.
- Flip switch // light on // true. There is no interaction with the user. For example, if you are trying to see if a user input a number instead of a String, that is no longer unit testing.
- Lower-level; testing individual pieces of code

With integration testing: Looking at a piece of code, maybe a class, and seeing how it affects the overall database system. How is it behaving with the rest of the system?
- Testing code from months ago; seeing how it runs with new code
- Make sure new code hasn't broken old code

Acceptance testing: Doing what you want. Sitting down with a user, business analyst--perhaps for hours or weeks--while the analyst places around as the user; interacting with things you haven't really thought of.
- User is accepting delivery and functionality of the system
- Many different ways to do it; sometimes no announcement is made because asking 15k users to see if they like the changes is too much. Usually devs just monitor the system for a few weeks to see if the number of tickets increases.