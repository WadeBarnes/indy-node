# Creating a DID using the Indy-CLI

You will need to perform the following commands once for each CLI machine that you want to run on. The following commands contain suggestions to save certain values in a secure place.  Please do not share those values or that place with anyone since you are the TRUSTEE. 

1. Start your indy-cli using the instructions from[Installing a CLI](./CLIInstall.md) for your platform. 
   All following commands are executing inside the cli.
2. Create a wallet with `wallet create wallet_name key=<wallet_key>`

   Where wallet_key is a secure key that only you should know. Quotes are not required for this key. Save it in a secure place for later use. You will use it every time you need to run Trustee commands.
3. `wallet open wallet_name key=<wallet_key>`
4. `did new seed=<SEED>`
   If you have lost your original seed or have never created one, then create a new one. This seed is used to regenerate your DID and to add your DID to your wallet(s).  
   The seed is a 32 character string that only you can know. 
   
   > WARNING: Whoever knows your Seed can recreate your exact DID in their own wallet and use it to manage the ledger.
   
   Save your Seed in a secure place so that only you can recreate your DID whenever needed.  
   Also save the public DID and verkey generated from this step so that you will know and can verify your public DID.
