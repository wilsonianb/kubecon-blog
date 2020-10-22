# kubecon-blog

My blog about my KubeCon talk, also my demo.

## Try it out

1. Fork this repository
2. Install an [OpenFaaS Cloud](https://docs.openfaas.com/openfaas-cloud/intro/) GitHub app to your forked repo
3. Copy the OpenFaaS Cloud [sealed secrets](https://docs.openfaas.com/openfaas-cloud/secrets/) `pub-cert.pem` file into the root directory of your repo.
3. Generate an ssh key pair:
```bash
ssh-keygen -t rsa -b 4096 -f ./id_rsa -N ""
```
4. Add the contents of the `id_rsa.pub` file as a [deploy key](https://developer.github.com/v3/guides/managing-deploy-keys/#setup-2) with **write access** for your forked repo.
5. Edit `stack.yml` values with your GitHub info.
6. Deploy:

```bash
export ADMIN_PASSWORD="" # To access the add-post function

# Replace username with your GitHub username
faas-cli cloud seal --name username-blog-secrets --literal admin-token=$ADMIN_PASSWORD --from-file=id_rsa

git add
git commit
git push
```

Whenever you add a post by add-posts, it will trigger a git commit, which triggers OpenFaaS Cloud, to publish a new version of the blog function.

Let's Thank Matias for his awesome blog post! Made our lives so much easy!
https://www.openfaas.com/blog/serverless-static-sites/
