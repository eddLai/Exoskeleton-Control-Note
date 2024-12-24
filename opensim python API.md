# Muscle analysis
要做muscle analysis需要設定muscle of interest
```python
muscle_analysis = osim.MuscleAnalysis()

# Set start and end times for the analysis.
muscle_analysis.setStartTime(first_time)
muscle_analysis.setEndTime(last_time)

# Set the muscle of interest (semitendinosus on the right leg).
muscle_list = osim.ArrayStr()
muscle_list.append("semiten_r")
```

設定分析
```python
muscle_analysis.setMuscles(muscle_list)

# Configure the analysis.
muscle_analysis.setOn(True)
muscle_analysis.setStepInterval(1)
muscle_analysis.setInDegrees(True)
muscle_analysis.setComputeMoments(True)
```

整合tool
```python
analyze_tool_normal_gait = osim.AnalyzeTool()
analyze_tool_normal_gait.setName("Muscle_Analysis_Normal_Gait")
```

Import model and motion file
```python
analyze_tool_normal_gait.setModelFilename("gait2392.osim")
analyze_tool_normal_gait.setCoordinatesFileName("normal_gait.mot")
# Add the MuscleAnalysis to the AnalyzeTool.
analyze_tool_normal_gait.updAnalysisSet().cloneAndAppend(muscle_analysis)
#result設定
analyze_tool_normal_gait.setResultsDir("MA_Normal_Gait_Results")
```

Configure AnalyzeTool.
```python
analyze_tool_normal_gait.setReplaceForceSet(False)
analyze_tool_normal_gait.setSolveForEquilibrium(True)
analyze_tool_normal_gait.setStartTime(first_time)
analyze_tool_normal_gait.setFinalTime(last_time)
```

save to XML
```python
# Print configuration of the AnalyzeTool to an XML file.
analyze_tool_normal_gait.printToXML("Muscle_Analysis_Normal_Gait_AnalyzeTool_setup.xml")
```

run analysis through XML
```python
# Load configuration and run the analyses. 
analyze_tool_normal_gait = osim.AnalyzeTool("Muscle_Analysis_Normal_Gait_AnalyzeTool_setup.xml", True)
result_normal_gait = analyze_tool_normal_gait.run()
```

