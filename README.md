# Verifying the Hardware Random Number Generator being used for the Raffle Bot
How to verify the authenticity of using the Hardware Random Number Generator for the Raffle Bot

## How it works
Each player joining the raffle is entered into a List.  
If the amount of players is five, then the first player is number 0 in the list, and the fifth player is number 4 in the list.  


Once all slots are filled up, the bot records what the current block number is and outputs it to the chat.  
It then sits and for the next block number (generally < 6 seconds). The next step is to store the number generated in that block by the HRNG.  
This is done to ensure that nobody has advance knowledge of the Hardware generated Random Number being presented.  
From the large number, it outputs a smaller number based on the amount of players.  


Go to the block in question to verify that the correct player won, for example: https://hpbscan.org/block/6699060  
There you see "Hardware Random Number" 0x146935869a8dc150faa5150746314d9b24f553ae271ebb3a91f135ae4ab55f26  
Run this python script:  
```
randomHex = "0x146935869a8dc150faa5150746314d9b24f553ae271ebb3a91f135ae4ab55f26"
randomNumber = int(randomHex, 16)
originalPlayerAmount = 5
minNumber = 0
maxNumber = 99999999999999999999999999999999999999999999999999999999999999999999999999999
mx = (randomNumber - minNumber) / (maxNumber - minNumber)
preshiftNormalized = mx * (originalPlayerAmount - minNumber)
shiftedNormalized = int(preshiftNormalized + minNumber)
print('Winning number is: {}'.format(shiftedNormalized))
```
