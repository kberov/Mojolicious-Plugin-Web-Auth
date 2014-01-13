# NAME

Mojolicious::Plugin::Web::Auth - Authentication plugin for Mojolicious

# SYNOPSIS

    # Mojolicious
    $self->plugin('Web::Auth'
        module      => 'Twitter',
        key         => 'Twitter consumer key',
        secret      => 'Twitter consumer secret',
        on_finished => sub {
            my ( $c, $access_token, $access_secret ) = @_;
            ...
        },
    );

    # Mojolicious::Lite
    plugin 'Web::Auth',
        module      => 'Twitter',
        key         => 'Twitter consumer key',
        secret      => 'Twitter consumer secret',
        on_finished => sub {
            my ( $c, $access_token, $access_secret ) = @_;
            ...
        };



    ### default authentication endpoint: /auth/{moniker}/authenticate
    # e.g.)
    # /auth/twitter/authenticate
    # /auth/facebook/authenticate
    ### default callback endpoint: /auth/{moniker}/callback
    # e.g.)
    # /auth/twitter/callback
    # /auth/facebook/callback

# DESCRIPTION

[Mojolicious::Plugin::Web::Auth](http://search.cpan.org/perldoc?Mojolicious::Plugin::Web::Auth) is authentication plugin for [Mojolicious](http://search.cpan.org/perldoc?Mojolicious).

# METHODS

[Mojolicious::Plugin::Directory](http://search.cpan.org/perldoc?Mojolicious::Plugin::Directory) inherits all methods from [Mojolicious::Plugin](http://search.cpan.org/perldoc?Mojolicious::Plugin).

# OPTIONS

[Mojolicious::Plugin::Web::Auth](http://search.cpan.org/perldoc?Mojolicious::Plugin::Web::Auth) supports the following options.

## `module`

This is a module name for authentication plugins.

Dropbox, Facebook, Github, Google, Instagram, Twitter.

## `key`

consumer key

## `secret`

consumer secret

## `scope`

optional. OAuth 2.0 only.

    # Facebook
    plugin 'Web::Auth',
        module      => 'Facebook',
        key         => 'Facebook App ID',
        secret      => 'Facebook App Secret',
        scope       => 'email,user_birthday',
        on_finished => sub {
            my ( $c, $access_token, $user_info ) = @_;
            ...
        };

## `on_finished`

    # Mojolicious::Lite
    plugin 'Web::Auth',
        module      => 'Twitter',
        key         => 'Twitter consumer key',
        secret      => 'Twitter consumer secret',
        on_finished => sub {
            my ( $c, $access_token, $access_secret, $user_ino ) = @_;
            ...
        };

This is a callback when authentication was finished.

### arguments

- OAuth 1.0(A)

    Dropbox, Twitter, etc.

    - Mojolicious::Controller
    - access\_token
    - access\_secret
    - user\_info ( enabled 'user\_info' )

- OAuth 2.0

    Facebook, Github, Google, Instagram, etc.

    - Mojolicious::Controller
    - access\_token
    - user\_info ( enabled 'user\_info' )

## `on_error`

This is a callback when authentication was errored.

# AUTHOR

hayajo <hayajo@cpan.org>

# CONTRIBUTORS

Many thanks to the contributors for their work.

- FAYLAND

# COPYRIGHT

Copyright 2013- hayajo

# LICENSE

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself.

# SEE ALSO

[Mojolicious](http://search.cpan.org/perldoc?Mojolicious), [Amon2::Auth](http://search.cpan.org/perldoc?Amon2::Auth)
