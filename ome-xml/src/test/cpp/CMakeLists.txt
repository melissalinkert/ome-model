# #%L
# OME C++ libraries (cmake build infrastructure)
# %%
# Copyright © 2006 - 2016 Open Microscopy Environment:
#   - Massachusetts Institute of Technology
#   - National Institutes of Health
#   - University of Dundee
#   - Board of Regents of the University of Wisconsin-Madison
#   - Glencoe Software, Inc.
# %%
# Redistribution and use in source and binary forms, with or without
# modification, are permitted provided that the following conditions are met:
#
# 1. Redistributions of source code must retain the above copyright notice,
#    this list of conditions and the following disclaimer.
# 2. Redistributions in binary form must reproduce the above copyright notice,
#    this list of conditions and the following disclaimer in the documentation
#    and/or other materials provided with the distribution.
#
# THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
# AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
# IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
# ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDERS OR CONTRIBUTORS BE
# LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
# CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
# SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
# INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
# CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
# ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
# POSSIBILITY OF SUCH DAMAGE.
#
# The views and conclusions contained in the software and documentation are
# those of the authors and should not be interpreted as representing official
# policies, either expressed or implied, of any organization.
# #L%

if(BUILD_TESTS)
  add_executable(color color.cpp)
  target_link_libraries(color OME::XML)
  target_link_libraries(color ome-test)

  add_executable(enum enum.cpp)
  target_link_libraries(enum OME::XML)
  target_link_libraries(enum ome-test)

  add_executable(constrained-numeric
                 non-negative-float.cpp
                 non-negative-integer.cpp
                 non-negative-long.cpp
                 percent-fraction.cpp
                 positive-float.cpp
                 positive-integer.cpp
                 positive-long.cpp)
  target_link_libraries(constrained-numeric OME::XML)
  target_link_libraries(constrained-numeric ome-test)

  add_executable(orderedmultimap orderedmultimap.cpp)
  target_link_libraries(orderedmultimap ome-test)

  add_executable(timestamp timestamp.cpp)
  target_link_libraries(timestamp OME::XML)
  target_link_libraries(timestamp ome-test)

  add_executable(transform transform.cpp)
  target_link_libraries(transform OME::Common OME::XML)
  target_link_libraries(transform ome-test)

  add_executable(transform-resolver transform-resolver.cpp)
  target_link_libraries(transform-resolver OME::Common OME::XML)
  target_link_libraries(transform-resolver ome-test)

  add_executable(model model.cpp)
  target_link_libraries(model OME::XML)
  target_link_libraries(model ome-test)

  add_executable(quantity
                 quantity.h
                 quantity.cpp
                 quantity-electricpotential.cpp
                 quantity-frequency.cpp
                 quantity-length.cpp
                 quantity-power.cpp
                 quantity-pressure.cpp
                 quantity-temperature.cpp
                 quantity-time.cpp)

  target_link_libraries(quantity OME::XML)
  target_link_libraries(quantity OME::Test Boost::iostreams)

  add_executable(version version.cpp)
  target_link_libraries(version OME::XML)
  target_link_libraries(version ome-test)

  ome_xml_add_test(ome-xml/color color)
  ome_xml_add_test(ome-xml/enum enum)
  ome_xml_add_test(ome-xml/constrained-numeric constrained-numeric)
  ome_xml_add_test(ome-xml/timestamp timestamp)
  ome_xml_add_test(ome-xml/transform-resolver transform-resolver)
  ome_xml_add_test(ome-xml/transform transform)
  ome_xml_add_test(ome-xml/model model)
  ome_xml_add_test(ome-xml/quantity quantity)
  ome_xml_add_test(ome-xml/version version)

  if(extended-tests)
    header_test_from_file(ome-xml OME::XML ome/xml)
    ome_xml_add_test(ome-xml/headers ome-xml-headers)
  endif(extended-tests)
endif(BUILD_TESTS)
