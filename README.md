# ssb-client-cli
Command Line interface to do basic things with [SSB](https://www.scuttlebutt.nz/)

## Inspiration
Many thanks to the authors of [ssb-client-basic](https://github.com/mixmix/ssb-client-basic) for their tutorials on accessing the SSB apis. They helped me understand a lot of what I've written here.

## Purpose
This repository is intended to expose SSB to the command line in a somewhat scriptable interface, provide a reference implementation of common tasks simple clients may want to do. The bulk of the code was written in one weekend so I expect it will be a bit rough around the edges, require some knowledge of the SSB. In most cases you're going to want to run this code next to a full SSB client, copy-paste hashes of various kinds to run the commands you want.

I've intentionally limited functionality to things exposed directly by [ssb-server](https://github.com/ssbc/ssb-server) in the first round but am not opposed to adding support for the most common plugins(friends, links, unread for instance). I don't expect this code to support all plugins or experimental plugins.

## Running
### Running in place
To run the programs in place, just run `npm install` to build dependencies, then `./bin/ssb-client [arguments]`

### Installing globally
To install globally run `npm install -g`. If you've configured npm in the standard ways this will put `ssb-client` on your path, allow you to run it from any shell as is listed in the examples that follow.

### Examples
```
# Tell people about yourself, attach a profile picture
ssb-client publish about --name 'Bob Smith' --description 'A handy guy' --image '&hashstring=.sha256'

# Post a message, mentioning another person
ssb-client publish post --text 'Weird things find you on the internet if you look too far. Right, [Mr Mime](@hashstring=.ed25519)?' --channel 'weirdness' --mentions '@hashstring=.ed25519'

# Print the last 5 messages on a channel
ssb-client query --type post --channel 'weirdness' --tail 5

# Print messages 5..10 in your feed
ssb-client query --author '@hashstring=.ed25519' --sequence 5..10

# Print messages posted in the last 24h
ssb-client query --type post --timestamp `date +%s000 --date='-24 hours'`..`date +%s000`

# List the available subcommands, options
ssb-client --help
ssb-client publish --help
ssb-client publish post --help
ssb-client query --help
```

## Contributing
If you find bugs feel free to report them as issues on this repo or fix them and PR your fixes. If you'd like to add functionality feel free to make PRs and I'll review them.

## License
This code is released under the MIT license, which should let you do almost anything with it. Have fun.
