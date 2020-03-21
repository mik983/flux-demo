# flux-demo
wget https://github.com/fluxcd/flux/releases/download/1.17.0/fluxctl_linux_amd64
sudo mv fluxctl_linux_amd64 /usr/local/bin/fluxctl

kubectl create ns flux

export GHUSER="mik983"
fluxctl install \
--git-user=${GHUSER} \
--git-email=${GHUSER}@users.noreply.github.com \
--git-url=git@github.com:${GHUSER}/flux-demo \
--git-path=namespaces,workloads \
--namespace=flux | kubectl apply -f -

kubectl -n flux rollout status deployment/flux

fluxctl identity --k8s-fwd-ns flux

fluxctl sync --k8s-fwd-ns flux
