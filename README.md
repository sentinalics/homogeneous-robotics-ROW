# homogeneous-robotics-ROW
mathematics in Codes

this code is about homogeneous matter in robotics
the problem is : this code is not working on my system but works on others

.
.
.

    D = 0.052
    
    dt = timestep/1000
    
    alpha = 0.0
    
    right wheel speed = 4.0
    left wheel speed = 4.5
    .
    .
    .
    angles = np.linspace(3.1415, -3.1415, 360)
    
    while robot.step(timestep) != -1:
        .
        .
        .
    
        rangers = np.array(lidar.getRangeImage())
        rangers[rangers == np.inf] = 0
        
        x_r, y_r = [], []
        x_w, y_w = [], []
        
                        
        w_T_r = np.array([
            [np.cos(alpha), -np.sin(alpha), xw],
            [np.sin(alpha), np.cos(alpha), yw],
            [0,0,1]])
        
        X_i = np.array([rangers* np.cos(angles), rangers* np.sin(angles) , np.ones((360,))])
        
        D = w_T_r @ X_i
        
        
        plt.ion()
        plt.plot(D[0, :], D[1,:], 'r.')
        plt.pause(0.001)
        plt.show()
        .
        .
        .
        .
        .
        .
        
        
        dist_r = radius * right wheel speed * dt
        dist_l = radius * left wheel speed * dt
        
        # #deltaomegaz (angular displacement)
        deltaomegaz = (dist_r - dist_l) / D
        
        # #alpha (Update cumulative heading  Radians)
        alpha += deltaomegaz
        
        # XW and YW
        xw += deltaX * np.cos(alpha)
        yw += deltaX * np.sin(alpha)
        
        # Monitor error relative to (0,0)
        error = np.sqrt(xw**2 + yw**2)
