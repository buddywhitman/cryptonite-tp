# Local Authority
## Solution
I looked up the page source to reveal the login.php POST request on form submission, and on reading through its code, I discovered references to `secure.js`, `styles.css` and `admin.php`.
Finally, after reading through the contents of all three, I found the correct pair of credentials, which I submitted to obtain the flag.

## Flag
`picoCTF{j5_15_7r4n5p4r3n7_b0c2c9cb}`

# Forbidden Paths
## Solution
I successively kept appending `../` to the relative path in the form, and eventually, the `file not found` error changed into the flag.

## Flag
`picoCTF{7h3_p47h_70_5ucc355_e5fe3d4d}`

# Caas
## Solution
I looked up the index.js file to realise that the `{message}` is not validated before being passed to exec and, thus, piped an `ls` after passing a random message as instructed in the front end. This revealed the existence of `falg.txt`, which I `cat`ed to obtain the flag.

## Flag
`picoCTF{moooooooooooooooooooooooooooooooooooooooooooooooooooooooooooo0o}`
