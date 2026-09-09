# Standalone build for the DRM client subsystem (PLAN H-002..H-005).
# The full MTA module is built via CMake; this Makefile compiles the DRM
# subsystem plus its unit tests without the MTA SDK, so it runs anywhere
# with g++ and OpenSSL (Linux x64 verified; H-006 matrix in docs/H-001).

CXX ?= g++
CXXFLAGS := -std=c++17 -Wall -Wextra -I source
LDLIBS := -lssl -lcrypto

DRM_SOURCES := source/drm/json.cpp source/drm/aead.cpp source/drm/ed25519.cpp \
               source/drm/base64.cpp source/drm/key_store.cpp \
               source/drm/http_client.cpp source/drm/license_client.cpp

.PHONY: test clean

test: /tmp/drm_test
	/tmp/drm_test

/tmp/drm_test: $(DRM_SOURCES) tests_drm/main.cpp
	$(CXX) $(CXXFLAGS) $(DRM_SOURCES) tests_drm/main.cpp $(LDLIBS) -o $@

clean:
	rm -f /tmp/drm_test
