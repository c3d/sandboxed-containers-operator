# hack/hcp — hypershift-cluster-setup (Prow publishing copy)

This directory is a publishing copy of the OSC team's `hypershift-cluster-setup`
script from `osc/scripts` (GitLab, private). It exists so Prow jobs in
`openshift/release` can fetch the script over public HTTPS — see the
`sandboxed-containers-operator-install-hcp-aws` workflow, which pulls
`HCP_SCRIPTS_REPO@HCP_SCRIPTS_REF` (this repository, branch
`feat/hcp-prow-testing`, path `hack/hcp`) at runtime.

Contents:

- `bin/hypershift-cluster-setup` — the script itself. Supports `--prow` to run
  inside a Prow multi-stage test step (non-interactive, state under
  `${SHARED_DIR}`, per-job cluster names from `PROW_JOB_ID`, cluster-profile
  AWS credentials/region/pull secret, CI registry credentials for `oc`).
- `lib/hypershift-cluster-setup-aws.sh` — AWS cloud library.
- `env/management-cluster-permissions-*.yaml` — scoped installer-role
  permissions used by `management create`.

The canonical home is `osc/scripts`; update this branch from there (bin/, lib/
and env/management-cluster-permissions-*.yaml) whenever the script changes:

    cp ../scripts/bin/hypershift-cluster-setup hack/hcp/bin/
    cp ../scripts/lib/hypershift-cluster-setup-aws.sh hack/hcp/lib/
    cp ../scripts/env/management-cluster-permissions-*.yaml hack/hcp/env/
