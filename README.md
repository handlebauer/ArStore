# ArStore

#### A framework allowing interested parties to adopt ArWeave incrementally for object storage. 

---

Let's take, for example, a Culturally Valuable Magazine. Currently, their editors use A Boring CMS to manage content and they persist their data on a cloud-based network. Increasingly, whispers have been spreading amongst literary circles about government activity around censorship. One of the younger guys on staff brings something called ArWeave to the attention of the CTO, who’s immediately excited by the notion of data permanence.  

She looks into it a bit. ArWeave is without question exciting but the ecosystem is still small. She notices the apps must be 10x less mature than even the most mill-run of cloud-based storage solutions. She fears the risks inherent to embracing a new technology and can’t help but feel wary of the cognitive barriers w/ re: to the mechanics/implementation. She knows right away they’re not ready to bring their whole operation over to the permaweb and wishes there were a simple, configurable WordPress plugin instead. At the point of content-submission, she would love it if editors could tick a box to upload sensitive works to the permaweb for safe keeping.

---

The obvious approach here is to build:

1. A UI to manage things like sign-ups and account settings. It would allow users to create their organization, generate schemas to describe the various shapes of their data (more of a stretch goal — the schemas could be used to validate data before committing it), as well as to view the current state of their data. The UI would be comparable to a headless CMS.

2. An API to handle the legwork. It would offer a dumbed-down interface vs. the current Arweave HTTP API in the hopes of encapsulating away as much as possible of the complexity necessary to interface with the chain, leveraging the account settings originally configured via the UI to prime the dev-facing convenience functions. 

Quickly, roughly:

```js
import ArStore from ‘ar-store’

const author = 'Jenny Offill'
const content = 'My question for Will is: Does this feel like a country at peace or at war? I’m joking, sort of, but he answers seriously. He says it feels the way it does just before it starts. It’s a weird thing, but you learn to pick up on it. Even while everybody’s convincing themselves it’s going to be okay, it’s there in the air somehow. The whole thing is more physical than mental, he tells me. Like hackles? The way a dog’s hackles go up? Yes, he says.'
const tstamp = new Date()

;(async () => {
  const { store, get, save } = await ArStore.login(process.env.WALLET_ADDRESS)
  console.log(store.organization) // Culturally Important Magazine
  const { id } = await save('fiction').data({ author, content, tstamp })
  const quote = await get('fiction').byId(id)
})()
```

---

ArWeave as well as blockchain-based tech in general are still new to me, so, questions:

1. Has this concept already been spoken for by someone else?
2. In terms of building a library, as sketched above, is it as simple as making a wrapper around the official ArWeave SDKs?

I think it would be particularly neat and important to bring this ease of use to those who would otherwise take a pass on ArWeave. There are obviously some UX challenges around how to manage payment and all of that. But I  believe the concept to be sound enough to make it worth those hurdles.  

I’d be happy to hear your thoughts, if you have some :—)

