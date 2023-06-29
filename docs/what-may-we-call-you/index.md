# What may we call you?


It shouldn't surprise you when I tell you that some websites are collecting too much data about you.
Aside from the obvious privacy issue, this is also a security issue.
You can invest in your security as much as you want and never be 100% safe, but:

> You cannot lose what you do not possess.

First of all, I have to admit that I made this mistake myself in one of my first projects.
I am writing this, so you don't have to make the same mistake.

## What's the matter?
I've once been working for a startup called [kiweno](https://kiweno.com/en/) which sells test kits for things like food intolerances.
Like many other websites, they want their users to create an account so all the information from various products can be linked together.
Here is what a part of the registration form looks like:

{{<image src="./kiweno-registration-form.png" src_l="./kiweno-registration-form-large.png" src_s="./kiweno-registration-form-small.png" caption="Registration form asking the user for forename, surname, phone number and gender">}}
The form is in German, because this company only targeted the german speaking market.
So in addition to asking for a username and a strong password, the page wanted to know your forename, surname, phone number and gender if you choose to tell them.

## What's wrong with that?

[Article 5 (c) of the GDPR](https://gdpr-info.eu/art-5-gdpr/) states that
> Personal data shall be: adequate, relevant and limited to what is necessary in relation to the purposes for which they are processed.

This is also called the **principle of data minimization**.
In simple terms, this means:
> Don't ask for more data than you need [for your product to work] 

To reiterate my point from the intro:  The less data you have, the smaller is the risk for your users, should your service get breached.
Let's look into what could be done better with this principle in mind.

### Communication channels
Of course, you almost always need some communication channel to contact your users, but one should be enough to sign up.
In the beginning, the phone number was not mandatory. 
To my surprise, the large majority of users still filled in this information since they were asked to.

Having only one input field that ask for **either email or phone** number might be a bit harder to process, but it would make it clear to the user that they do not have to provide both.
The option to fill in the other form of contact could be added on a profile page.

### Why even ask for a gender?

In the case of the gender field, the option to not answer is even preselected.
Still, against the default bias, the large majority gave away this information.
Given the medical context, some users might be confused whether this field requires their biological gender, or the gender they identify with.
In both cases there are to few options.

There are some products of kiweno now where your biological gender is required to get a better result.
However, the actual explanation as to why this is already asked at signup is (as so often in software) for legacy reasons.

In the beginning, the assumption was to require this information to correctly address people in e-mails and other form of communication.
Since in German you would use "Sehr geehrter Herr" / "Sehr geehrte Frau" in place of "Dear".
Later, the marketing team made the great decision to drop this formal tone and use a more informal you ("du", which is gender-neutral in German) to address users.

> Get rid of your prototypes while you can, or they will haunt you.

### Names are hard

Having two separate fields for fore- and surname gives the impression that a user's real name is required.
This might be the case for a bill or shipping address, but - depending on how purchases are processed - this might never need to be persisted in your own system.
I would recommend any startup to let your payment provider deal with this kind of data.

Similar to the gender, the name fields were initially introduced to address users correctly in email conversations.
But again, it is not that simple for all people.
Not every culture uses names the same way.
E.g.: In Spain it is common two have two surnames, one of each parent.
Read the [wikipedia](https://en.wikipedia.org/wiki/Personal_name) if you want to go all the way down this rabbit hole.

If the real name of a user is not important to you for legal reasons, I would recommend you to use a single text field asking them *"What may we call you"*.
Make sure you reserve enough space in your database so especially my Austrian folks can enter all their acumulated titles.

## How could we do better?
If there is no immediate use of the data for your product, don't ask for it in advance.

Be aware of how you communicate to your users what kind of data you require from them.

Make it obvious how important or unimportant the accuracy of every field is.
E.g.: don't use a date picker for a birthdate, when the year suffices.

Even if your only target a specific market (e.g.: only German-speaking users), be mindful of users of other cultures that might also are a part of this group.
