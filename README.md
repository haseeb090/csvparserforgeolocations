# csvparserforgeolocations

Introduction

CSV files i.e. comma separated value files are widely used in order to store data. This program parses one such file and stores the relevant data in a map.
Approach

The Java file created consists of a class that has a map. This map stores all the relevant data.
/*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package aplab3;

import java.io.*;
import java.util.*;

/**
 *
 * @author Haseeb Khizar
 */

public class APlab3 {

    static void displaydata(Map<String, Float[]> cd) { //to display map of integer key and string array value
        for (String key : cd.keySet()) {
            Float[] x = cd.get(key);
            System.out.print(key + " ");
            System.out.print("Lat: " + x[0] + " ");
            System.out.print("Long: " + x[1] + " ");
            System.out.println();
        }
    }

    /**
     *
     * @param args
     */
    public static void main(String[] args) {
        Map<String, Float[]> citydata = new HashMap<String, Float[]>(); //create map of string key of cityname and array int of latitude and longitude points
        String csvFile = "GeoLiteCity-Location.csv";
        String line = "";
        String csvSplit = ",";
        try (BufferedReader br = new BufferedReader(new FileReader(csvFile))) {//buffered reader to parse csv file
            line = br.readLine();//skip the first line of the csv
            line = br.readLine();//skip the second line of the csv
            while ((line = br.readLine()) != null) {//loop to parse through lines of the csv
                String[] country = line.split(csvSplit);//splitting the whole line into a string array
                if (country[3].length() == 0) {//if condition to check if city column entry is empty or not
                    continue;
                }
                Float[] points = new Float[2];//array to store coordinates of a city
                //System.out.println(Float.parseFloat(country[5]));
                //System.out.println(Float.parseFloat(country[6]));
                String[] x = country[5].trim().split("\\s+");
                try {
                    points[0] = Float.parseFloat(country[5].trim().split("\\s+")[0]);//storing latitude
                    points[1] = Float.parseFloat(country[6].trim().split("\\s+")[0]);//storing longitude
                } catch (Exception e) {//Exception to handle string """" in file
                    e.printStackTrace();
                }
                String city = country[3];//story city into a string
                citydata.put(city, points);//put the key and the rest of the columns as value into the map
            }

            displaydata(citydata);

        } catch (IOException e) {
            e.printStackTrace();
        }

    }

}
How to Run

The java File is to be simply run with the Geo lite file in the project directory.

