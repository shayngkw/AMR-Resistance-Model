def run_model(allocation_function,cost,mutation):

    import random
    import math
    import matplotlib.pyplot as plt
    import sys
    import inspect
    import pandas as pd
    
    
    
    ## Two antibiotics, A and B
    ## Four genotypes (resistant or not to each drug) + uninfected hosts
    
    t_max = 5000 # number of timesteps for model
    
    n_patients = 1 # number of patients in hospital
    
    beta = 0.05 # transmission rate
    clearance = 0.01 # clearance rate
    efficacyA = 0.01 # efficacy of antibiotic A
    efficacyB = 0.005 # efficacy of antibiotic B
    mortality = 0.01 # death rate from infection
    costA = cost # cost of carrying resistance mutation A
    costB = cost # cost of carrying resistance mutation B
    mutation = mutation # rate at which infections change genotype
    
    # vectors to store results    
    uninfected = list()
    sensitive = list()
    resistant_A = list()
    resistant_B = list()
    resistant_AB = list()
    deaths = list()
    usage_A = [1]
    usage_B = [1]
    
    
    # set initial conditions
    sensitive.append(1-(clearance+mortality)/beta)
    resistant_A.append(0) #.1*(1-(clearance+mortality)/beta)
    resistant_B.append(0)
    resistant_AB.append(0)
    uninfected.append(n_patients - sensitive[0] - resistant_A[0] - resistant_B[0] - resistant_AB[0])
    deaths.append(0)
    
    
    for i in range(1,t_max):
        # decide how much of each drug to use
        allocation=allocation_function(i, sensitive[i-1], resistant_A[i-1], resistant_B[i-1], resistant_AB[i-1])
        A=allocation[0]
        B=allocation[1]
        # if statement to make sure they don't use more drugs than is possible
        if(A+B>1):
            A=0
            B=0
        # implement difference equations
        sensitive.append(sensitive[-1] + beta*sensitive[-1]*uninfected[-1] - (A*efficacyA + B*efficacyB + clearance + mortality)*sensitive[-1] - 2*mutation*sensitive[-1] + mutation*resistant_A[-1] + mutation*resistant_B[-1])
        resistant_A.append(resistant_A[-1] + beta*resistant_A[-1]*uninfected[i-1] - (B*efficacyB + clearance + mortality + costA)*resistant_A[-1] + mutation*sensitive[-1] + mutation*resistant_AB[-1] - 2*mutation*resistant_A[-1])
        resistant_B.append(resistant_B[-1] + beta*resistant_B[-1]*uninfected[i-1] - (A*efficacyA + clearance + mortality + costB)*resistant_B[-1] + mutation*sensitive[-1] + mutation*resistant_AB[-1] - 2*mutation*resistant_B[-1])
        resistant_AB.append(resistant_AB[-1] + beta*resistant_AB[-1]*uninfected[i-1] - (clearance + mortality + costA + costB)*resistant_AB[-1] + mutation*resistant_B[-1] + mutation*resistant_A[-1] - 2*mutation*resistant_AB[-1])
        if (sensitive[-1]<0):
            sensitive[-1]=0
        if (sensitive[-1]>1):
            sensitive[-1]=1
        if (resistant_A[-1]<0):
            resistant_A[-1]=0
        if (resistant_A[-1]>1):
            resistant_A[-1]=1
        if (resistant_B[-1]<0):
            resistant_B[-1]=0
        if (resistant_B[-1]>1):
            resistant_B[-1]=1
        if (resistant_AB[-1]<0):
            resistant_AB[-1]=0
        if (resistant_AB[-1]>1):
            resistant_AB[-1]=1
        #Now lists are updated -  so index -1 points to updated value for this iteration
        uninfected.append(n_patients - sensitive[-1] - resistant_A[-1] - resistant_B[-1] - resistant_AB[-1])
        # record deaths
        deaths.append(100000*mortality*(sensitive[-1]+ resistant_A[-1]+ resistant_B[-1]+ resistant_AB[-1]))
        # record drug usage
        usage_A.append(A)
        usage_B.append(B)
        
    time_point=range(0,t_max)
        
    out_data = pd.DataFrame(
        {'day': time_point,
         'usage_A': usage_A,
         'usage_B': usage_B,
         'sensitive': sensitive,
         'resistant_A': resistant_A,
         'resistant_B': resistant_B,
         'resistant_AB': resistant_AB,
         'deaths': deaths
         })
    output_data=out_data.iloc[1:]
    return output_data   
