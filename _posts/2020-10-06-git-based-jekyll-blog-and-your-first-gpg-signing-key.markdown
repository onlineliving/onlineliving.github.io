---
layout: post
title:  "Git-Based Jekyll Blog and Blog Signing Key"
date:   2020-10-06  
categories:              
---
### Before you get started

#### OS
- Kali GNU/Linux

#### GitHub Prerequisites
- Create your account [GitHub Sign Up Page][github-signup].
- Verify your GitHub email address. Check your inbox.
- Create your new repository [GitHub Create New Repository][github-new-repo].

#### Blog Signing Key Prerequisites
- GnuPG `gpg --version`

#### Jekyll Prerequisites
- Ruby version 2.5.0 or higher `ruby -v`
- RubyGems `gem -v`
- GCC and Make `gcc -v` `g++ -v` `make -v`


### Blog Signing Key

#### GPG Key Generation
`$ gpg --full-generate-key`
- You want the `RSA and RSA (default)` selection. Select it by simply pressing `Enter`.
- You want a key size of 4096 bits. Select it by entering `4096` and pressing `Enter`.
- You want your key to never expire. Select this by pressing `Enter`. Confirm this by entering `y` and pressing `Enter`.
- You want to give GnuPG you real name so that it can construct your user ID. Do this by entering your real name at the prompt.
- The same for your email address. You want to give GnuPG the same email address associated with your verified GitHub email address.
- You want to comment on this GPG key. Here you can comment on what type of GPG key this is i.e. Blog Signing Key.
- You want to select Okay. Do this by entering `o` and pressing `Enter`.

#### Add GPG Key to Your GitHub Account
You want to print the GPG Key ID that you just generated in a format that GitHub can understand. You start by accessing your unique GPG Key ID. You can use this GPG Key ID in a gpg command to print it in ASCII Armor Format. This will help GitHub understand your GPG Key and it will allow you to sign your Git commits. GitHub will verify that your Pushes to your remote GitHub repository are signed with your verified signature.

##### Access Your GPG Key ID

`$ gpg --list-secret-keys --keyid-format LONG`

Example output

	/home/username/.gnupg/pubring.kbx
	------------------------------------
	sec   4096R/3AA5C34371567BD2 2020-10-06 [SC]
	uid                 [ultimate] Real Name (Comment) <Email Address>
	ssb   4096R/42B317FD4BA89E7A 2020-10-06 [E]

##### Print the GPG Key ID in ASCII Armor Format

`$ gpg --armor --export 3AA5C34371567BD2`


	-----BEGIN PGP PUBLIC KEY BLOCK----


	-----END PGP PUBLIC KEY BLOCK-----

You want to copy everything between the two markers including the markers.

##### Add the GPG Key to Your GitHub Account

From GitHub account's homepage, make the following selections 

`Settings > SSH and GPG keys > New GPG key` 

From the above section, paste the `PGP PUBLIC KEY BLOCK` in the field named `GPG Keys`. 


### Configuring Git to Allow Signing Your Commits with GPG Key

#### Set Your Blog Signing Key in Git 
`$ git config --global user.signingkey 3AA5C34371567BD2`

#### Add Your Blog Signing Key to Your Bash Profile
`$ test -r ~/.bash_profile && echo 'export GPG_TTY=$(tty)' >> ~/.bash_profile`

`$ echo 'export GPG_TTY=$(tty)' >> ~/.profile`

#### Cloning Your Remote Repository to Your Local Repository with Git

	kali@kali:~/projects/blog$ git clone https://github.com/username/username.github.io.git

#### Configuring Git with Your GitHub Credentials	
	kali@kali:~/projects/blog$ cd username.github.io
	kali@kali:~/projects/blog/username.github.io$ git config --global user.name "username"
	kali@kali:~/projects/blog/username.github.io$ git config --global user.email you@example.com
	kali@kali:~/projects/blog/username.github.io$ git config commit.gpgsign true


### Jekyll

#### Jekyll and Bundler Gems

kali@kali:~/projects/blog/username.github.io$ 

`sudo gem install jekyll bundler`

#### Create Your New Jekyll Site

kali@kali:~/projects/blog/username.github.io$ 

`sudo jekyll new .`

#### Build Site and Host it from Localhost:4000

You want to open a new terminal and navigating your filesystem to the blog's local repository before executing the following command.

kali@kali:~/projects/blog/username.github.io$ 

`sudo bundle exec Jekyll serve`

#### Customization

Browse to `localhost:4000` to view your blog. You might want to customize your blog.  


### Signing Your Blog's Changes with Signed Commits & Pushing Your Blog's Changes to GitHub

#### Add

kali@kali:~/projects/blog/username.github.io$ 

`git add --all`

#### Signed Commit

kali@kali:~/projects/blog/username.github.io$ 

`git commit -S -m "Customized Git-Based Jekyll Blog"`

#### Push to GitHub

kali@kali:~/projects/blog/username.github.io$ 

`git push -u origin master`

[github-signup]: https://github.com 
[github-new-repo]: https://github.com/new 

