import os
import arcpy
from arcpy import env
try:
    arcpy.env.overwriteOutput = True  
    env.workspace = "H:/Desktop/Exam_Data/Exam_Data"
    buf = 50
    unit = 'meters'
    dataset = 'points'
    
    inFC = arcpy.GetParameterAsText(0)
    buf = arcpy.GetParameterAsText(1)
    unit = arcpy.GetParameterAsText(1)
    fcName = os.path.basename(inFC) 
    fcName = os.path.splitext(fcName)[0]
    
    arcpy.CreateFileGDB_management("H:/Desktop/Exam_Data/Exam_Data/", "new.gdb")
    path = os.path.join("H:/Desktop/Exam_Data/Exam_Data", 'new.gdb')
    outFC = os.path.join("new.gdb", fcName)
    arcpy.CreateFeatureDataset_management(path,dataset)
    datasetpath = os.path.join(path, dataset)
    buf_dis = str(buf)+ unit
    desc = arcpy.Describe(inFC)
    if desc.shapeType == "Polygon":
            arcpy.CopyFeature_management (inFC, "C:/Data/new.gdb/" + desc.basename)
            arcpy.Buffer_analysis(inFC, outFC, buf_dis, "FULL", "FLAT", "PLANAR","ALL","")
            arcpy.AddMessage('Buffer creater') 
            arcpy.AddField_management(inFC, "CORE_AREA", "DOUBLE")
            arcpy.AddField_management(inFC, "CORE_PERC", "DOUBLE")
            
            geometryField = arcpy.Describe(outFC).shapeFieldName 
            
except:
    print arcpy.GetMessages()
