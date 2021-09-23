
"""Created on Fri Apr 19 12:53:54 2019

@author: bichaudh
description: CSV Read and create multiple polygon from ID and add field as ParcelID
"""
try :#Import libraries
    import arcpy, os
    import csv
    from arcpy import env


    #set environment and initialization
    env.workspace = "H:/Desktop/Exam_Data/Exam_Data"
    env.overwriteOutput = True
    gdb = "Result.gdb"
    fc = "polygon.shp"
    i=0
    j=0
    sf = arcpy.SpatialReference("NAD 1983 UTM Zone 10N")
    path = os.path.join("H:/Desktop/Exam_Data/Exam_Data", gdb)
    #create GDB
    arcpy.CreateFileGDB_management("H:/Desktop/Exam_Data/Exam_Data", gdb)
    arcpy.CreateFeatureclass_management("H:/Desktop/Exam_Data/Exam_Data", fc, "Polygon" )
    arcpy.AddField_management(fc, "PARCEL", "TEXT", field_length = 20)
    cursor = arcpy.da.InsertCursor( fc, ["SHAPE@"] )
    array = arcpy.Array( )
    point = arcpy.Point( )
    #file open
    with open(r'H:\Desktop\Exam_Data\Exam_Data\parcelpoints.csv', 'r') as csvfile:
        csvfile.readline() 
        reader = csv.reader(csvfile)
        cursor = arcpy.da.InsertCursor(fc, ["SHAPE@","PARCEL"])
        header = reader.next()
        for row in reader:
            j=j+1
            point.ID, point.X, point.Y = row[0], row[1], row[2]
            array.add(point)
      
            if ((i != row[0]) and (i!=0))or (j==len(row)):
                print row[0]
                ID = arcpy.Polygon(array,sf)
                cursor.insertRow([ID,i])
                array.removeAll()
    	i = row[0]
    del cursor
except :
    print "error"
