export NAME=cozyplane-kpr
export NAMESPACE=cozy-cozyplane

include ../../../hack/common-envs.mk
include ../../../hack/package.mk

# The lllamnyp/cozyplane ref charts/cozyplane-kpr is vendored from, verbatim. Keep the
# three cozyplane packages on the same ref; Cozystack's settings live in this
# wrapper, never in the vendored chart.
COZYPLANE_REF=453eb6509c78a792d1fab5f5166ef3fa0e4c7942

test:
	helm unittest .

update:
	mkdir -p charts && tmp=$$(mktemp -d charts/.update.XXXXXX) && \
	{ curl -fsSL https://github.com/lllamnyp/cozyplane/archive/$(COZYPLANE_REF).tar.gz | \
	  tar -xzf - -C "$$tmp" --strip-components=3 cozyplane-$(COZYPLANE_REF)/chart/cozyplane-kpr || \
	  { rm -rf "$$tmp"; exit 1; }; } && \
	rm -rf charts/cozyplane-kpr && mv "$$tmp" charts/cozyplane-kpr
