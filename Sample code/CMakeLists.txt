cmake_minimum_required(VERSION 3.22)
project(VstAiDemo VERSION 1.0.0)

# JUCE is fetched automatically at configure time. Requires internet on first build.
include(FetchContent)
FetchContent_Declare(JUCE
  GIT_REPOSITORY https://github.com/juce-framework/JUCE.git
  GIT_TAG 8.0.8
  GIT_SHALLOW TRUE)
FetchContent_MakeAvailable(JUCE)

juce_add_plugin(VstAiDemo
  COMPANY_NAME "Iron Circuit Audio"
  BUNDLE_ID "audio.ironcircuit.vstaidemo"
  PLUGIN_MANUFACTURER_CODE IrCa
  PLUGIN_CODE Sm60
  FORMATS VST3 Standalone
  PRODUCT_NAME "Smasherman 6000"
  IS_SYNTH FALSE
  NEEDS_MIDI_INPUT FALSE
  NEEDS_MIDI_OUTPUT FALSE
  IS_MIDI_EFFECT FALSE
  EDITOR_WANTS_KEYBOARD_FOCUS FALSE
  COPY_PLUGIN_AFTER_BUILD FALSE)
juce_generate_juce_header(VstAiDemo)

target_sources(VstAiDemo PRIVATE
  Source/PluginProcessor.cpp
  Source/PluginProcessor.h
  Source/PluginEditor.cpp
  Source/PluginEditor.h)

target_compile_features(VstAiDemo PRIVATE cxx_std_17)
target_compile_definitions(VstAiDemo PUBLIC
  JUCE_WEB_BROWSER=0 JUCE_USE_CURL=0 JUCE_VST3_CAN_REPLACE_VST2=0)
target_link_libraries(VstAiDemo PRIVATE
  juce::juce_audio_utils
  juce::juce_dsp
  PUBLIC juce::juce_recommended_config_flags
         juce::juce_recommended_lto_flags
         juce::juce_recommended_warning_flags)
