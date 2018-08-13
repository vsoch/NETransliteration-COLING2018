# Tensorflow experimental (with containers)

To replicate the study fully, please see the [README.md](../README.md) that describes
setting up resources with AWS Deep Learning. This description will generate (to the
best of the author's ability) a comparable environment that is agnostic to the host
provider, and requires Docker (or Singularity) container technologies.

You will be building the container from the [root of the repository](../) and direct to the
Dockerfile that you want, depending on needing (or not being able to use) GPU. Let's be
honest, everyone **needs** gpu (*wink*).

```bash
# no GPU
docker build -t vanessa/netransliteration-coling2018-cpu -f docker/Dockerfile .

# no GPU
docker build -t vanessa/netransliteration-coling2018-gpu -f docker/Dockerfile.gpu .
```

**More coming soon!** I'm sleepy.

