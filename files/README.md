# Changes from EMUX

## launcher-ludus

Line 41, replaced call to `dialog` with argument of the script

## run-emux-docker-ludus

Line 18, changed port forwards to be the same on the host as in the container for 1:1 port pass through to allow for users to connect to telnetd after exploitation
Line 32, replaced `-it` with `--detach` for headless running

