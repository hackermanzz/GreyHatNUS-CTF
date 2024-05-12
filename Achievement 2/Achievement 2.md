
Achievement 2 require us to purchase all items in the shop for the flag to be unlocked. 
![[Pasted image 20240504172837.png]]

However, when browsing the shop for the first time we meet a vagabond-looking cat with a purple hoodie on select various trinkets and potions. These items increase in value exponentially and the last time even has a requirement to purchase all other products before unlocking it.

![[Pasted image 20240504172909.png]]

We can earn coins through the `flappy cat` minigame. To earn coins we have to navigate our kitty through openings in the pipes, each successful point awards us 10 coins! Personally my high score is 1337420 :).

![[Pasted image 20240504172925.png]]

Now that we have earned some coins, we are able to afford some of the trinkets in the shop. It would take too much time to manually earn the coins to purchase everything. So lets use cheat engine to change that.

![[Pasted image 20240504173310.png]]

After firing up cheat engine and selecting the game's process to open. We can conduct an initial scan for the current amount of coins that we have: `620`. Setting the value type to `float` and scanning for the exact value of `620`, we are able to discover 2 addresses that contain those values.

![[Pasted image 20240504173244.png]]

Double clicking on each entry allows us to change their values. As an example lets change the address `1B9E29668C0` value to `10000`. To do this, double click on the value column and enter the desired value into the pop-up input field. Press `ok` to execute the update.

![[Pasted image 20240504173437.png]]

Our coins will not change immediately and will require a revisit. By clicking `back` and re-entering the shop we can see our updated coins value. Now we have 10000 coins! 

However, 10000 is just enough to purchase the almighty powerful fire-cat crystal (yellow orb). Hence, we need more!!!

![[Pasted image 20240504173456.png]]

Hopping back to Cheat engine, lets add more funds to our coin pouch. We will be using an extremely large number just for good measures in case the last item is exorbitantly expensive.

![[Pasted image 20240504173529.png]]

Boom! We're rich enough to afford the entire shop. I think vagabond cat would be very happy because of us. 

![[Pasted image 20240504173538.png]]

![[Pasted image 20240504173557.png]]

After buying out the shop, we can collect our flag back at the `achievements` page.

```
grey{unl1m1t3d_m0n3y_unl1m1t3d_p0w3r_kl2j1fd}
```

![[Pasted image 20240504173609.png]]

Another interesting thing about the number of coins is that if the value is too large, it will simply be replaced with a positive infinity symbol. This would be reflected back in the game's shop as well. Way to be the richest in cat galaxy.

![[Pasted image 20240504173714.png]]

![[Pasted image 20240504173727.png]]
