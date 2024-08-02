# MedHacks
Code used to activate peripheral sensors to measure head dimensions and to calculate coordinates for activating transmitter units.
The following python code is used by peripheral sensors on the helmet to first measure the distance between the furthest points in the xy and yz planes individually. By doing so, the head dimesnions can be known.

import math

def euclidean_distance_xy(point1, point2):
    """Calculate the Euclidean distance between two points in the xy-plane."""
    return math.sqrt((point1[0] - point2[0])**2 + (point1[1] - point2[1])**2)

def euclidean_distance_yz(point1, point2):
    """Calculate the Euclidean distance between two points in the yz-plane."""
    return math.sqrt((point1[1] - point2[1])**2 + (point1[2] - point2[2])**2)

def max_distance_xy(points):
    """Find the maximum distance between any two points in the xy-plane."""
    max_dist = 0
    for i in range(len(points)):
        for j in range(i + 1, len(points)):
            dist = euclidean_distance_xy(points[i], points[j])
            if dist > max_dist:
                max_dist = dist
    return max_dist

def max_distance_yz(points):
    """Find the maximum distance between any two points in the yz-plane."""
    max_dist = 0
    for i in range(len(points)):
        for j in range(i + 1, len(points)):
            dist = euclidean_distance_yz(points[i], points[j])
            if dist > max_dist:
                max_dist = dist
    return max_dist

After calculating the furthest distance between the peripheral sensors, the transmitters in the required region can be activated by the following code:
import math

def euclidean_distance_xy(point1, point2):
    """Calculate the Euclidean distance between two points in the xy-plane."""
    return math.sqrt((point1[0] - point2[0])**2 + (point1[1] - point2[1])**2)

def euclidean_distance_yz(point1, point2):
    """Calculate the Euclidean distance between two points in the yz-plane."""
    return math.sqrt((point1[1] - point2[1])**2 + (point1[2] - point2[2])**2)

def max_distance_xy(points):
    """Find the maximum distance between any two points in the xy-plane and return the points."""
    max_dist = 0
    p1_extreme = None
    p2_extreme = None
    for i in range(len(points)):
        for j in range(i + 1, len(points)):
            dist = euclidean_distance_xy(points[i], points[j])
            if dist > max_dist:
                max_dist = dist
                p1_extreme = points[i]
                p2_extreme = points[j]
    return max_dist, p1_extreme, p2_extreme

def max_distance_yz(points):
    """Find the maximum distance between any two points in the yz-plane and return the points."""
    max_dist = 0
    p1_extreme = None
    p2_extreme = None
    for i in range(len(points)):
        for j in range(i + 1, len(points)):
            dist = euclidean_distance_yz(points[i], points[j])
            if dist > max_dist:
                max_dist = dist
                p1_extreme = points[i]
                p2_extreme = points[j]
    return max_dist, p1_extreme, p2_extreme

def divide_point(point1, point2, m, n):
    """Divide the line segment between two points in the ratio m:N and return the dividing point."""
    x1, y1, z1 = point1
    x2, y2, z2 = point2
    total = m + n
    x = (m * x2 + n * x1) / total
    y = (m * y2 + n * y1) / total
    z = (m * z2 + n * z1) / total
    return (x, y, z)



