# The duty to forget


## What's the issue this time?
I recently checked [Have I Been Pawned](https://haveibeenpwned.com/) to see where my email addresses have been leaked.
(You should do so as well after reading this!)
Unsurprisingly my data was part of various data leaks.
But there was one thing all the leaks had in common that made me think.
All the sources that failed to keep my data private are services I don’t even use anymore.

Now you could argue why I didn’t delete these accounts after I stopped using them, and you would be right.
I have to blame myself as well.
However, as I looked into my password manager and saw I amassed over 150 accounts over the years.
That’s quite a lot to keep track of, and I am not even counting all the services that are to connect to my Google or similar accounts.

### Deleting accounts can be hard
If you're not already using a password manager, I recommend you better start using one right now.
But even if you can keep track of all your accounts and regularly go through them, deleting an account can be challenging.
You probably know the saying:
> If you love something, set it free. If it comes back, it’s yours. If not, it was never meant to be.

[Some services](https://twitter.com/lurking_alpaca/status/1407933907367043074) understood this and made it as simple to delete your account as it is to sign up for a new one.
Others, however, try their best to hide this feature, as if their revenue would depend on it.

### GDPR to the rescue
For all Europeans, there is a backdoor to remove your data from any service, which comes in the form of the [GDPR](https://gdpr-info.eu/).
More specifically, [Article 17](https://gdpr-info.eu/art-17-gdpr/), or as it is often referred to, the “right to be forgotten,” allows you to have your data deleted should it not be used anymore.

Now, I know from the times I had to use this myself that it can still be a burdensome process.
Thomas Landauer probably had the same impression, which is why he created [Online-Kündigen.at](https://www.online-kuendigen.at/).
This fine website contains templates and the right addresses to send your deletion request to for most services in Austria and beyond.

### Get a copy of your data
If you're curious about what data a service has stored about you, there is also [Article 15](https://gdpr-info.eu/art-15-gdpr/) of the GDPR, which allows you to get a copy of just that.
Additionally, you can ask about the purpose your data is used for and much more.
What sparked my interest is section 1.d), which states that you are allowed to know:
_“...where possible, the envisaged period for which the personal data will be stored, or, if not possible, the criteria used to determine that period;”_
To which you'll most likely get the answer: _“We will store your data until further notice.”_
But what if I am no longer able to give that notice?

## Call of duty
To recap: As a European citizen (and in countries with similar laws), there is always a way to get your digital traces removed, but there is still one missing feature that I would wish online services need to implement.
Instead of the **right to be forgotten**, I would like to flip the responsibility of deleting unused data and make it a **duty to forget**.

If you're a Software Developer yourself, you can probably imagine how hard it will be to convince your product managers to implement a feature that automatically deletes inactive accounts.
Still, I think there are good reasons to do it before it is enforced by law (which it hopefully will be someday).
First, let me explain what exactly I imagine this feature to be.

### As a user, I want to be forgotten so I can have peace of mind.
I have been in more than one meeting where a lengthy discussion was ended by simply pointing out that _“We are not like Google.”_
This revelation is probably not a hard pill to swallow for most software developers out there.
Yet, it should not prevent us from observing how tech giants operate and learn from them.
After all, there is a reason they're giants.
They might have done some things right up until now.

So here is how Google handles deleting inactive accounts.
There is a menu in the account settings called [Inactive Account Manager](https://myaccount.google.com/inactive).
Here you can decide after how many months your account should be treated as inactive.
This means if you didn’t use any of their services for the set period, you will get notified that your account will be marked as inactive.
At this point, a person you appointed can take over the control of your account or download a copy of your data.
If this person does not respond or you did not designate someone, your data will be deleted after another 3 months.

{{<image src="./inactive-account-manager.png" src_l="./inactive-account-manager-large.png" src_s="./inactive-account-manager-small.png" caption="Screenshot of the inactive account management settings page">}}

Transferring the ownership of a user’s data goes beyond just being forgotten and rather represents something like a digital last will.
However, the inactivity and deletion part should be relatively simple to implement on its own.
Adding two timestamps (`LAST_ACTIVE_AT` and `DELETE_BY`) in the user database and a cron job to set and act on them should do the trick.

Yes, I glossed over the `deleteUser()` process itself, which ‒ depending on how ~~micro~~ distributed the underlying services are ‒ might be a bit trickier.
I argue, though, that this function should already be in place since any kind of service should allow its users to trigger it themselves anyway.

Trust me when I tell you that you really want to automate the deletion of users.
This is coming from someone who had to answer Article 17 requests (see above) by manually dropping the right rows of the production database.
It’s a nightmare nobody should have to go through.

## Economics
Let’s get back to why any service provider should implement this.
After all, the user value behind this feature is quite vague.
What is hopefully a bit easier to comprehend is the amount of money the IT department spends on infrastructure (should this not be the case in your company, think about changing your hosting provider).
It should be evident to everyone that an ever-growing amount of data can only lead to an ever-growing cost for storage (independent if it is self-hosted or not).

Furthermore, an ever-growing index in a database means a steady decline in query performance which impacts all users.
Both examples' effect is “just” logarithmic, but the trend is still in the wrong direction.

In German, there is a word for inactive members.
They're called _Karteileiche_, literally meaning a _corpse in the register_. So if you want to sell this to your product manager, tell them you want to eliminate all those zombies slowing down your service.

## Privacy by design
A slightly less disturbing argument is to stay compliant with ISO standard 31700-1:2023, also known as **privacy by design** (yes, it was also news to me that this has a standard).
This concept was written up in 1995 and is based on 7 principles. The first one being:
> Proactive not reactive; preventive not remedial

Think back to my initial issue.
There is not much a company can do for me once my data has leaked, but there is a lot that can be done to prevent it from happening in the first place.
There are plenty of guidelines and regulations around security, and by all means, you should make sure [the front doesn't fall off](https://www.youtube.com/watch?v=3m5qxZm_JqM), but undoubtedly the most secure measure is to ensure there is nothing left that can leak at all.

## TL;DR
If you're in charge of user data, make sure it is the **default** procedure to delete it after a certain period of inactivity. Tell your users about this and inform them before it takes effect.

### Homework
Now I have one more piece of homework for you. Go through your password manager (which you should have set up by now) and check old entries. Are you still using that account? If not, get it deleted. You can't do it yourself? Send a mail referring to Article 17 in the subject line.

---

## PS: A word about the Catholic Church
I did my homework as well and checked the oldest entries inside my password manager.
It turns out the oldest one belongs to [a website of the catholic church](https://www.meinbeitragzaehlt.at/Login) meant to enter data about salary so they can more accurately calculate one's church tax.

It just so happens that I quit my membership with this organization quite some time ago, but my login to this page still worked, so I got curious about what else they might have stored about me.
It also triggered me that the password is my 8-digit account number, which I can’t change, so please don’t hack me.

They answered my Article 15 request within days by sending me a PDF of 8 printed and subsequently slightly slanted scanned spreadsheets.
This was entirely on-brand for an organization of their age, but the promptness of the response made me wonder how often they get requests like mine.

Overall the contents of the report were not surprising since I never went as far as giving them information about my salary, but there is other information they gathered even without me handing it to them.
For instance, my last home addresses, which are now outdated but are still nothing I would need to be leaked. 
After giving it a second read, there was one more thing in it that caught my attention.

### The court case
As if they were expecting my next message, they included a court case where someone like me wanted to have their data deleted ([DSK 16.11.2007, K121.309/0010-DSK/2007](https://www.ris.bka.gv.at/Dokumente/Dsk/DSKTE_20071116_K121309_0010_DSK_2007_00/DSKTE_20071116_K121309_0010_DSK_2007_00.html)). This is from a time when Austria still had a different data protection act (the DSG 2000), but the fundamentals were pretty close to the GDPR.

The issue here is that two constitutionally protected rights are at odds here. The right to be forgotten and the right of the church not to have its internal affairs influenced by the state. The church keeps parish registers to record anyone who ever received a sacrament. Since, according to their rules, you can only get baptized once, they need to keep track of you.

Even if you decide to leave, they want to keep you as a _member in spirit_, should you ever change your mind and want to have a church wedding or any other sacrament.
In the end, the court ruled in favor of the church, arguing that the DSG 2000 does not intend to eradicate collective memories of society, and removing someone from the parish registers would come close to that.

You could use the same argument to allow Blizzard to save your World of Warcraft account indefinitely because someone might want to marry your Draenei paladin in the future.
The only difference is that World of Warcraft is not an official religion... yet.
Going just by the membership count, it should, though.
At the time of writing this post, World of Warcraft had around [127 million subscribers](https://mmo-population.com/r/wow/stats).
In contrast, Sikhism has 26 million members worldwide, and it is an official religion in Austria.

Even though I do not collect any data about you, I'll keep you all as _readers in spirit_.
And remember: Thou shalt not share your data.
Now go forth in privacy.

