- Feature Name: crate_name_transfer
- Start Date: 2018-12-15
- RFC PR:
- Rust Issue:

# Summary

This experimental RFC proposes a process by which a designated group of Rust team members
could reassign ownership of a crate name on crates.io. The aim is to
identify the absolute smallest, most conservative step we can feasibly make from
the status quo of crate names that can only be transferred by a current owner.
The proposal is intended to address *only the absolute most clear-cut
situations* in which a crate name would need to be transferred. It is not
intended to address the situation of name squatting on crates.io, nor as a
gateway to eventual more aggressive forced exchange of crate names.

# Motivation

It is my humble belief that there exists such a thing as a clear-cut situation
in which transferring a crate name from one person to another makes sense.

The following situation describes a real crate (all of the following describe
the same crate):

- Crate was last updated 4 years ago,
- Not a single version of the crate compiles on any Rust compiler 1.0.0 or
  newer,
- In the most recent version of the crate, the author has indicated that the
  entire crate is deprecated,
- Zero other crates depend on the crate,
- Crate has a desirable name that a different user is eager to use for a library
  that is all ready to be published,
- Reasonable efforts to contact the author are unsuccessful.

This eRFC introduces an opportunity for a group of Rust team members to be entrusted in
volunteering their time and their reputation to improve the experience of using
crates.io by arbitrating similarly clear-cut cases.

# Experiment

This RFC proposes evaluating the process outlined below as an experiment that
can be abandoned at any time with or without cause.

Any Rust team (core team, or subteam with representation on the core team) is
welcome to call off the experiment at any time if they perceive undesired
fallout from the experiment, or for any reason whatsoever. Such a decision would
be arrived at by that team's ordinary decision-making / consensus-reaching
process. The safeword is as follows:

> The [your-team-name] team believes it would be better to discontinue this
> experiment and would like to stop fulfilling crate transfer requests effective
> immediately.

No justification needs to be given; the activities described in this RFC will
terminate without further discussion.

This termination condition is intended as a lightweight way to avert or contain
unforeseen impact of adopting this experimental RFC.

The experiment will continue indefinitely until terminated as described here or
amended by another RFC.

<!-- TODO: Add review meeting after 6 months. -->

# Reference-level explanation

The library team and/or moderation team will appoint a group of 3 to 5 people
as the "crates.io crate name transfer team".
This team will be a sub team of the "crates.io team".
<!-- TODO: rename team members should be considered crates.io team members.
    Do they get voting rights, the right to raise concerns in RFCs? -->
Crate transfers happen at the sole discretion of the "crates.io crate name transfer team".

Transfer requests are approved if a majority of the team members approves the
request and none object to it.
<!-- TODO: This is the same decision making method as other teams follow
  is there a more detailed description we can refer to. -->
<!-- TODO: Are votes public? -->

To reiterate: crate transfers happen at the sole discretion of the team. 
There is no checklist of criteria that decide whether a request is
granted. The team is entrusted with upholding the intent of the
eRFC in performing transfers in only the absolute most clear-cut cases according
to their judgement.

When a user requests ownership of a crate, the two possible responses by the
team are:

1. All right, we yanked the existing releases and set you as the owner! Please
   ensure that the next version you publish is a separate semver major version
   from any of the old yanked releases.

2. Hi! Thanks for the request. We believe this case is less clear-cut than the
   ones we are currently willing to grant. We would recommend picking a different
   crate name for now, but we can leave this request open if you want and
   revisit the decision in the future.

The team is encouraged to respond to requests in a timely manner,
but realistically they will respond when they have time and mental energy
available.

# Guide-level explanation

The details of requesting ownership of a crate name are to be figured out over
time, but a viable way to begin would be as follows.

- Implement the appropriate [audit trail in crates.io][audit] to provide ground
  truth if a dispute should arise.

- Modify crates.io, so that it only allows the new owners of a crate to publish
  versions of the new crate which are semver-incompatible to those of the old crate.

- After a crate was transferred display a banner for 90 days on it's crates.io page
  informing visitors of the change in ownership.

- Set up a repository under https://github.com/rust-lang called
  "crate-transfers".

- Write a readme outlining the process. Ensure that the readme conveys that only
  the most clear-cut requests will be granted, so not to expect too much.

- Requests are made by filing a GitHub issue.

- Include a list of "up for grabs" crate names in the readme. Authors that no
  longer wish to use a crate name that they own can add it to the list by filing
  an issue or sending a pull request. A crate that is "up for grabs" trivially
  meets the "clear-cut situation" requirement if ownership of that name is ever
  requested.

- Crate name transfers are executed by a crates.io operations person.

- Decision to terminate the experiment may be delivered by filing an issue
  containing the safeword message above. A pre-prepared note will be added to
  the readme and the repository will be [archived].

[audit]: https://github.com/rust-lang/crates.io/issues/1548
[archived]: https://help.github.com/articles/about-archiving-repositories/

# Drawbacks

### What if people get mad at the name transfer team?

People are welcome to get mad at any Rust team member at any time, although this
is not encouraged. The Responsible Party needs to be willing to stake their
reputation on their ability to make sound decisions, and must be willing to take
the fall if things go bad. Some experiments fail.

Checks and balances exist, particularly as any Rust team may terminate the
experiment with or without cause.

### What recourse is available if somebody is unhappy with a decision?

The usual:

- Complain on Twitter.
- Blog about it.
- Strategically upvote and downvote on Reddit.
- Email the mods.
- File lawsuit.
- ...

None of this is different from any other team decision that may make a person
unhappy -- the libs team breaking your code, or the moderation team deleting
your flame war for example.

### This RFC does not go far enough.

This eRFC is not intended as a solution to the name squatting situation on
crates.io. This eRFC does not denounce the behavior of registering crate names
without the intention of using them.

By taking this step, it may be perceived as a decision *against* ever addressing
the name squatting situation more decisively. That is not the intention of this
eRFC.

It may be perceived as a decision *against* adopting a namespacing scheme or
other mechanism of shrinking the occurrence of package name contention. Likewise
not the intention of this eRFC. I would encourage anyone believing strongly in
namespacing to pursue it in a different RFC. Namespacing touches on an
overlapping set of concerns but is orthogonal to this RFC in that we may opt to
do neither, one or the other, or both.

By design, this eRFC proposes making the smallest and most conservative possible
step from the status quo.

### The volume of requests may be overwhelming.

If the volume of requests is overwhelming, that would be sufficient reason for
a team or the Responsible Party to terminate the experiment.

Rather than "let's not try this experiment because there is a possibility there
will be too many requests," I would recommend that you please see it the other
way around: "let's try this experiment because there is a possibility that there
will *not* be too many requests."

If there are overwhelmingly many requests, this RFC puts us under no obligation
to hire some kind of large paid support staff to work through them. A
lightweight termination condition returns us to the status quo, after which we
can revisit in another RFC better informed by our newfound knowledge.

### Why would anyone volunteer to be a Responsible Party?

Two volunteers expressed interest in the pre-eRFC thread on the internals forum
(disclosure: one of them is the RFC author). I believe this is already
sufficient to move forward with the RFC.

If in the future it becomes impossible to find willing qualified candidates,
this would be sufficient reason for a team to terminate the experiment, which
immediately returns us to the status quo. Note that a gap in coverage does not
automatically terminate the experiment. Termination would be a team decision
based on the negatives of having the process continue to exist without a person
behind it, as well as the perceived likelihood of a qualified candidate turning
up in time.

# Rationale and alternatives

### Alternative: provide a checklist of criteria

"The crate must be X years old, must not have crates depending on it, must be
below version 1.0, must ..."

I believe it is better to leave the decision entirely up to judgement of the
Responsible Party with no checklist. Similarly, the lang team does not have a
checklist that determines what language changes are made ("must use no more than
two new keywords, ...").

Under this RFC, crate transfers happen at the sole discretion of the Responsible
Party. Purely as a place to maintain record of the bikeshed on possible
criteria, here is a non-exhaustive list of factors that one might expect could
influence the decision:

- How many years since last release was published.
- How long since owner has engaged in any public way with the repository.
- Whether there exists any stable or nightly Rust compiler 1.0.0 or newer that
  can successfully compile the crate.
- Statement by the owner that they no longer want the crate name.
- Announcement by the owner that the crate is abandoned.
- Code that couldn't possibly be useful to anyone for any purpose.
- Reasonable efforts to contact the owner have been unsuccessful.
- Number of dependent crates.
- Prominence of dependent crates.
- Reputation of requester.
- Requester has code ready to be published.
- Requester is the chronologically first person to have requested the name.

It is not necessary to debate this list because this list has no bearing on the
proposal of this RFC, which is that crate transfers happen at the sole
discretion of the Responsible Party. Let's debate the list only after deciding
that there should be a list.

### Alternative: Single person responsible party

An earlier version of this RFC proposed that one person is sufficient to 
handle crates.io crate name transfers.

Arguments to proceed with one person and not a team:

- The responsible party is encouraged by the design of the experiment to
  be as cautious and conservative as possible.
- A new team adds overhead to the decision-making process.
- There may not be enough volunteers to form a team.
- The Responsible Party may always seek the advice of Rust team members in
  borderline cases without there being an official second designee.

# Prior art

### npm

https://www.npmjs.com/policies/disputes

- Name squatting is against the Terms of Use. Squatted packages (as assessed by
  a human) are eligible for immediate transfer to another user who asks for it.

- Outside of squatting, users wanting to request transfer of a package name are
  required to contact the existing author with cc to support@npmjs.com.

- In case of no amicable resolution within 4 weeks, support staff arbitrate the
  dispute entirely at their discretion and judgement.

Like in this RFC, resolution is ultimately at the discretion of staff and not
governed (at least not publicly) by a criteria checklist.

We know from @ashleygwilliams (source: she worked at npm for 3 years) that npm
has a large paid support staff that spends 80+% of its time handling package
disputes. Manually handling package disputes is a huge drain on their time. Some
may hold this as a reason not to pursue this RFC. I see it as the opposite. If
"do nothing" were a viable plan, npm would surely have thought of it and be
saving their money instead. The service provided by their dispute resolution is
so valuable to the health of their ecosystem that it is worth paying so much
for.

### PyPI

https://www.python.org/dev/peps/pep-0541/

PEP 541 "Package Index Name Retention" was [accepted] in March 2018 but a
precise workflow is still being developed. Implementation is tracked in
[pypa/warehouse#1506].

Under this policy, name squatting is disallowed and squatted packages are
removed on sight.

Outside of name squatting, transfer requests are only granted for abandoned
packages. The staff does not participate in disputes around active packages. A
project is considered abandoned when all of the following are met:

- owner not reachable across 3 attempts over 6 weeks
- no releases within the past 12 months
- no activity from the owner on the project's home page

If a candidate appears willing to continue maintenance on an abandoned project,
ownership of the name is transferred when all of the following are met:

- candidate demonstrates failed attempts to contact the existing owner
- candidate demonstrates improvements on their own fork of the project
- candidate justifies why a fork under a different name is not an acceptable
  workaround
- the maintainers of the Package Index have no additional reservations

An abandoned project can be transferred to a new owner for purposes of reusing
the name when all of the following are met:

- candidate demonstrates failed attempts to contact the existing owner
- candidate demonstrates that the project suggested to reuse the name already
  exists and meets notability requirements
- candidate justifies why selecting a different name is not an acceptable
  workaround
- download statistics indicate that the existing package is not being used
- the maintainers of the Package Index have no additional reservations

[accepted]: https://mail.python.org/pipermail/distutils-sig/2018-March/032089.html
[pypa/warehouse#1506]: https://github.com/pypa/warehouse/issues/1506

### Other

I am interested to hear experiences from any other package ecosystems!

# Unresolved questions

Let me know!

# Future possibilities

This eRFC would like to avoid, as much as possible, any association with a name
squatting policy. Such a policy should be a largely orthogonal RFC.

As much as this is not the objective of this eRFC, the way this experiment plays
out will likely inform any future policy on squatting.
