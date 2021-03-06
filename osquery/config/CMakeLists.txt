#  Copyright (c) 2014-present, Facebook, Inc.
#  All rights reserved.
#
#  This source code is licensed under both the Apache 2.0 license (found in the
#  LICENSE file in the root directory of this source tree) and the GPLv2 (found
#  in the COPYING file in the root directory of this source tree).
#  You may select, at your option, one of the above-listed licenses.

ADD_OSQUERY_LIBRARY(TRUE osquery_config
  config.cpp
  packs.cpp
)

file(GLOB OSQUERY_CONFIG_PLUGINS "plugins/*.cpp")

ADD_OSQUERY_LIBRARY(FALSE osquery_config_plugins
  ${OSQUERY_CONFIG_PLUGINS}
  update.cpp
)

file(GLOB OSQUERY_CONFIG_PARSERS "parsers/*.cpp")
ADD_OSQUERY_LIBRARY(TRUE osquery_config_parsers
  ${OSQUERY_CONFIG_PARSERS}
)

file(GLOB OSQUERY_CONFIG_TESTS "tests/config_tests.cpp")
ADD_OSQUERY_TEST(TRUE ${OSQUERY_CONFIG_TESTS})

# The packs tests will attempt to execute SQL, they must be additional
file(GLOB OSQUERY_PACKS_TESTS "tests/packs_tests.cpp")
ADD_OSQUERY_TEST(FALSE ${OSQUERY_PACKS_TESTS})

file(GLOB OSQUERY_CONFIG_PLUGIN_TESTS "*/tests/*.cpp")
ADD_OSQUERY_TEST(FALSE ${OSQUERY_CONFIG_PLUGIN_TESTS})
