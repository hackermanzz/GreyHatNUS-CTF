# Grey Cat's Adventure!!!

These challenges requires players to utilize a wide range of techniques to capture the flags. Firstly, players need to understand the basics of cheat engine and how to modify arbitrary values to bypass certain requirements in the game. Players are also required to think out of the box for some challenges that may seem impossible.

This write-up will be beginner friendly. This is because, it was also my first time using cheat-engine and had to learn everything on the go :).

# Timelock

`Timelock` is the first minigame that players will encounter. It features a count down of 50 hours that claims will reveal the flag once it is completed. 

### Challenge

![Uploading timelock.png…]()

The starting value of the game will be `180000`. With every second the value will decrement by 1. However, players will be quick to realize the counting will pause if the game is out of focus. Furthermore, the game itself warns players that the counter will reset if they left that screen.

### Solution



# Vault

`Vault` is a minigame that players will encounter in the landing page. When the player enters the vault, they will encounter 2 screens cycling through characters very quickly. The screens will then come to a standstill indicating that the sequence of characters is complete. 

### Challenge

If you were to blink you may miss the entire sequence of characters and just be met with 2 `X` characters. 

![end](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/765ae6d9-a12c-4da2-bc9c-72aa91996985)


  be quick to notice that if they were to un-focus from the application, it will pause the cycling and freeze in time. Players that are even quicker may discover the first few characters are `E`,`Y`,`{` connoting that the values may eventually construct the flag.

![Clue](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/6624934e-8626-4d51-9803-9fdfbf80e469)


### Solution

If speed is the issue, lets remove it! We can start a screen recording right before clicking on the `vault`. We can slow down the footage once completed to reveal the flag!



https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/1669ac1d-4205-43c8-aea8-0cee9d284a55




Do keep in mind the last 2 `X` characters are not to be confused with the flag. They are simply just filler characters to tell the players that the sequence has ended.

The assembled string should look something like that:

```
grey{t_numb3r5_m450n_wh4t_d0_th3y_m34n??!}
```

Its a small reference to the Call of Duty Black Ops but we can see that it clear is incomplete. After a little trial and error, we end up with the complete flag.

```
grey{th3_numb3r5_m450n_wh4t_d0_th3y_m34n??!}
```

Hopefully, they found out what the numbers meant...

![8pq7o3](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/66a65686-1a3d-4f23-a494-dc090b8899de)


# Achievement 1

This challenge introduces the `flappy cat` game. The achievement's description requires us to get a high score of exactly 1337420, nice. 

![1](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/0a64dbb3-7040-47af-9cb7-68c1433f5a98)

Since our high score starts from 0, if we were to conduct a new scan for `0` we would have too many values to look through and it'd be impossible to find the address that correlates to the high score.

However, we can use the `next scan` method to keep track of changing values. We can start with a scan for the value `0` since our high score is currently `0`.

![2](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/3b3cb8d7-26bf-4138-bdc6-366b023e98b9)

 Cheat engine retrieved 82,000,000 million possible addresses that could hold our high score. We can lower the number of possible addresses by utilizing the `Next Scan` feature from cheat engine.

![3](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/a6d98255-8e58-47c4-8819-21111685da5b)

For our next value lets get a highscore of `1` and scan for the exact value `1`. This should narrow down the number of addresses significantly. Right now I have narrowed it down to roughly 47 thousand possible addresses. That is still a large amount of manually sift through. 

![4](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/48c0cb8e-659a-49e6-875f-526f274647a6)

Lets continue to update our highscore to `2` and run another scan for the exact value `2`. This should considerably reduce the amount of possible addresses. 

![5](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/cc100815-e55e-46f7-b126-1df4177fdce5)

Using the same method, I was able to pinpoint the exact address required that holds the value for the game's high score. This took me considerably longer as I was struggling to increase my high score lol; It's much harder than it looks!

![6](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/415003c8-f333-4e17-8e25-6443157158d6)

In our cheat engine menu, we can change the value that the address holds by double clicking on it and entering a different integer value. In this case, the achievement requested for exactly `1337420` (nice).

![7](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/8cc10ae8-f6d6-4325-8c84-66e72341a45a)


The update should reflect accordingly once we focus back into the application (I actually played the game for this high score, source: trust me bro).

![8](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/cdc3aaef-8aa0-4bb9-a8d7-8578917737f2)


We can then collect our flag in the achievements screen. Nice job gamers :D. 

![9](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/c1fd8977-f3a1-40ef-9430-384de0fb4d0c)


# Achievement 2

Achievement 2 require us to purchase all items in the shop for the flag to be unlocked. 

![1](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/266d477b-b988-45d2-89f3-d4ec43d52baa)


However, when browsing the shop for the first time we meet a vagabond-looking cat with a purple hoodie on select various trinkets and potions. These items increase in value exponentially and the last time even has a requirement to purchase all other products before unlocking it.

![2](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/ba186e2f-f602-4219-9f17-92b41efede8c)


We can earn coins through the `flappy cat` minigame. To earn coins we have to navigate our kitty through openings in the pipes, each successful point awards us 10 coins! Personally my high score is `1337420` :).

![3](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/bf1ba354-717d-47f2-b375-7d40b938df95)


Now that we have earned some coins, we are able to afford some of the trinkets in the shop. It would take too much time to manually earn the coins to purchase everything. So lets use cheat engine to change that.

![4](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/37893b19-445d-4936-91d9-b659dee8e32c)


After firing up cheat engine and selecting the game's process to open. We can conduct an initial scan for the current amount of coins that we have: `620`. Setting the value type to `float` and scanning for the exact value of `620`, we are able to discover 2 addresses that contain those values.

![5](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/67f088dc-6e1d-40be-a1e2-88fcc1a80383)


Double clicking on each entry allows us to change their values. As an example lets change the address `1B9E29668C0` value to `10000`. To do this, double click on the value column and enter the desired value into the pop-up input field. Press `ok` to execute the update.

![6](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/8d77f7bb-0f56-4ac2-9561-523e0f686806)


Our coins will not change immediately and will require a revisit. By clicking `back` and re-entering the shop we can see our updated coins value. Now we have 10000 coins! 

However, 10000 is just enough to purchase the almighty powerful fire-cat crystal (yellow orb). Hence, we need more!!!

![7](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/95c81392-121f-4c40-9d85-b8ae656172e8)


Hopping back to Cheat engine, lets add more funds to our coin pouch. We will be using an extremely large number just for good measures in case the last item is exorbitantly expensive.

![8](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/afff7acb-ec53-4404-9e56-fb691f5bc0bc)


Boom! We're rich enough to afford the entire shop. I think vagabond cat would be very happy because of us. 

![9](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/dd202111-0226-4760-a957-4110ffb4354a)

![10](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/e4e1e2bb-02d5-48ac-b0fc-c1dbb92acc61)


After buying out the shop, we can collect our flag back at the `achievements` page.

```
grey{unl1m1t3d_m0n3y_unl1m1t3d_p0w3r_kl2j1fd}
```
![11](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/29021b30-5d31-4fb3-8af6-6d5318a60985)


Another interesting thing about the number of coins is that if the value is too large, it will simply be replaced with a positive infinity symbol. This would be reflected back in the game's shop as well. Way to be the richest in cat galaxy.

![12](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/6c30ff18-21fc-44a3-bf88-0ae31f9f53a6)

![13](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/8f4d9720-cd70-46c2-8ccf-828266c3e0fe)


# Achievement 3

The 3rd achievement points us in the direction of the credits in search for a secret message. As we read through the credits, we can see several unorthodox symbols between the lines.

![1](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/32a61b2c-37c5-4d1d-a02b-f366725bfe69)

![2](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/494eb651-7a7f-4a33-830f-0ee174ebac2d)

![3](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/3fca4f8f-ca38-4e9b-a2d7-33a2c7eb99b0)


As the credits roll, we confirm that only three symbols were used: `-`, `.` and `X`. This looks very similar to morse code. However, morse code does not use `X` but instead a `space` is used. We can substitute all `X` characters with a `space` and decode them accordingly

The resulting cipher text should look something like this:

```
--. .. --/. .- -.-. ./- - --. .. --/. .- -.-. ../.. .- -..
```

Keep in mind, in most morse code translators, the forward slash `/` is used to denote spacing between new words.

The resulting plain text when converted:

```
GIGACATGIGACHAD
```

![4](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/23eb9f98-92a7-4337-85fc-de04edab8d36)


We still need to enter this into the input field at the bottom of the achievements screen to get our flag.

![5](https://github.com/hackermanzz/GreyHatNUS-CTF/assets/55987051/9195faa7-a9a0-4399-adbc-1e159694cc56)


