# Crack to find secret 
Install `jwt-cracker` from npm. `npm i jwt-cracker`.

Run the program using various wordlists to find the secret.
```bash
jwt-cracker -t <jwt> -d <wordlist>
```
RockYou.txt works fine. Also there is a special wordlist for jwts, `jwt.secrets.list`

For more wordlists, refer to this collection [SecLists](https://github.com/danielmiessler/SecLists/tree/master)