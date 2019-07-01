# windows10 ssh-agent
```
/c/Users/cuiyuqiang/.ssh
cuiyuqiang@HQ-TS-0146 MINGW64 ~/.ssh
$ ssh-add -L
Could not open a connection to your authentication agent.

$ exec ssh-agent bash

$ eval ssh-agent -s
SSH_AUTH_SOCK=/tmp/ssh-X7xYRlizpAut/agent.33268; export SSH_AUTH_SOCK;
SSH_AGENT_PID=29268; export SSH_AGENT_PID;
echo Agent pid 29268;

$ ssh-add -L
The agent has no identities.

$ ssh-add id_rsa_github
Identity added: id_rsa_github (id_rsa_github)

$ ssh-add -L
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQDuLpqpkw+jIi9oTpXmheA+KT4ICOOWhzRdjWBo7LWLHe/ZPNoZE8vEG0k/vWKour2BR4h0FMYkSFS4/uWLKKTVFSNVJ4/fD6lN8MFE+iyCroislk2z3aL43ETsRJ0n0xs8h2YGB+Kho1izlijU9VKZx3lvR9W7LUHYZzJGVU5DBFcN/CCF4P/4vDG+CM47coqg9ljNsf6cKF/LIp1YisTFKVa1WJ7NKIdIbNB+hhyRjZpOoVHClGO76DqWeP4y2wtcIE/yOVBZylWLYHt/e/ScLZtixHbCA2US4FQRiTP8EYvl6ZyYMw2bs0To3vEjO7C28UUiv2m31H0RgCEFevUpNPK69bXvGl99TD+SQHYIM6ww+VArux2itkX5PUDOr2eqhtSvlRu+ZUrrD9w6ssJey9Kf9EdthGumUh9n93fpuXNTEKzO4TQK9IEQneOxkeNxngCeJTQ35O97yymreiY6TvCiMQgDN6zAUVFUTqxbd2wNkcxQHO9HC2HqGT3jOG/pBrwvvOOmTJ0F/cv2MeiRd7HWx7QeGhkyPavPly13g8BV7kpu9f3UgKeXoiEWJrmOOP91RajYJVGIkGgkJMYDKV3ayGL6cBy4aM9YE9hKC4DZsdN7fiYy+BvvJEuWLDqzjkF1jsWFLoNLxilweg8fHK4GR0RRyItCEChVVkZbvw== id_rsa_github

```