
// LIBRARIES
import processing.pdf.*;


// GLOBAL VARIABLES
PShape baseMap;
String csv[];
String myData[][];

// SETUP
void setup() {
  size(555, 606);
  baseMap = loadShape("India-locator-map-blank.svg");
  csv = loadStrings("IAF_Revised_Data-Table 1.csv");
  myData = new String[csv.length][5];
  for(int i=0; i<csv.length;i++){
    myData[i]= csv[i].split(",");
  }
}


// DRAW
void draw() {
  beginRecord(PDF,"IAF_PDF_PLEASE_SAVE3.pdf");
  shape(baseMap, 0, 0, width, height);
  
  for(int i=0; i<myData.length;i++){
    noStroke();
      fill(255, 0, 0, 70);
      float graphLong = map(float(myData[i][3]), 67, 97.5, 0, width);
      float graphLat= map(float(myData[i][2]), 38, 7.5, 0, height);
      //float markerSize = 0.05*sqrt(float(myData[i][6]))/PI;
      //println(graphLong+ "/" + graphLat + "/" +markerSize +"/"+ float(myData[i][6]));
     float temp = float(myData[i][6])*5;
     ellipse(graphLong, graphLat, temp+15, temp+15);
    }
    float legendLong = map(79.5, 67, 97.5, 0, width);
    float legendLat= map(10, 38, 7.5, 0, height);
    for (int i=0;i<10;i++){
      float temp1 = i*5;
      ellipse(legendLong, legendLat, temp1+15, temp1+15);
      legendLong = legendLong + temp1+13;
    }
  endRecord();
  println("PDF Saved.");
 }
