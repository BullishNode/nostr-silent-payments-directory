# nostr-silent-payments-directory
Silent Payments Nostr Directory with On-chain zaps using BTC, LBTC and L-USDt

There is demonstrated demand for re-usable payment codes for Bitcoin payments. LNURL, Bolt12 and BIP47 have had varying degrees of adoption and success. These are features Bitcoin users generally find attractive. This is a concept that has gained popularity in the fiat fintech world. Think of cashtags in cashapp, paypal addresses, and even SINPE phone numbers in Costa Rica. People prefer to interact with short aliases rather than bank accounts and public keys. 

Reusable payment addresses are useful for:
- donation pages 
- mining pool payouts 
- Bitcoin exchange withdrawals 
- payroll 

For mainnent Bitcoin transactions ("on-chain") they act as an alternative to reused Bitcoin addresses which are extremely bad for privacy. 

The case of BIP47 is interesting. It did not get a lot of traction outside of Samourai Wallet. The reason for Samourai’s success was the concept of Paynym, a directory for BIP47 payment codes which abstracted the payment code with a memorable alias. As we have seen with Samourai, a centralized director of re-usable payment codes is fragile and not sustainable. 

Nostr seems a well-suited alternative to a centralized payment code directory. Indeed, an undeniable key feature of nostr is Zaps. The user experience to send money to anyone using their nostr pubkey as the payment destination has proven to be a success. The Nostr network acts as a lightning network address director so that Bitcoin users do not need to request payment instructions from another Nostr user they wish to pay, they can just query the network of Nostr relays to find an event which maps a Lightning Network address to a nostr public key.

I believe that we need alternatives to Lightning Network for payments on Nostr. I don’t need to go into details and even statistics. I think it is generally accepted that most lightning payments are being performed via custodial wallets and that self-custodial lightning has significant operational and user experience issues. Self-custodial bitcoin network transactions do not suffer from these issues. Liquid network transactions also do not suffer from these issues. 

What I propose is a NIP that allows nostr users to publish a silent payment address as part of their nostr profile. To pay someone else, simply retrieve the event from an npub that published the silent payment address and derive a new Bitcoin address. The nostr network or relays becomes the silent payments directory. 

To create a Zap-like experience, here is what I propose:
- Bob publishes a Bitcoin or Liquid network silent payment address. Bob can also specify what kind of assets he wishes to accept as payments (i.e. BTC, L-BTC and L-USDt)
- This could even work with Ark, assuming Ark also implements silent payments addresses. 
- Alice requests silent payment address from Bob’s npub from the network of Nostr relays and looking for the specific event type that maps Bob's public key to his silent payments address.
- Alice derives a Bitcoin address or Liquid address from Bob’s silent payments addresses
- Alice sends a payment to that address
- Alice sends a DM to Bob telling bob “I sent you (x) amount to your address, here is the txid”
- Bob’s wallet scans for the payment, and checks that he indeed got a transaction id with that amount. He can safely assume that the payment is indeed from Alice.

While it is not necessary to broadcast this to the entire network for privacy, Alice can also publish this event openly on the Nostr Network.
Bob can acknowledge that he indeed got the payment from Alice.

Note: even without publishing it openly on the network, it is useful for Alice to be able to tell bob via DM that she paid Bob. Otherwise, Bob would not know who the payment is form.

The drawback of on-chain payments is of course that Bitcoin network fees are expensive. However, this can be solved by using the Liquid Network.

The Liquid network has gained a lot of traction. There are multiple wallets and SDKs that have integrated it:
Green
Bull Bitcoin
Aqua
CoinOS
BTCPay Server
Breez SDK
Helm
Marina

In order to make this proposal work, we need to port the Silent Payments concept to Liquid. It can work with the Bitcoin network, but only high-value payments would be economical. And of course most payments on Nostr (and most payments in everyday life) are low-value payments.

A cool benefit of this is that it would enable USDt-denominated payments. While I am not a fan of fiatcoins personally, I think its undeniable that many people are. L-USDt has some interesting characteristics, notably that because of Confidential Transactions and Payjoin it offers some good privacy, and compared to the other blockchains Liquid is orders of magnitude more censorship-resistant.

The end result is that a Bitcoin wallet can integrate nostr and offer a payments UX where the sender will select a npub from his contact list with a username and simple “send an on-chain payment to that username”. A really good UX can be achieved without a custodial wallet and without the hassle of self-custodial lightning. 

Bull Bitcoin is willing and able to support this initiave, an idea by myself (Francis Pouliot).



