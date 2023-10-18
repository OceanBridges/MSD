import numpy as np
import matplotlib.pyplot as plt
from dataclasses import make_dataclass
import pandas as pd
import seaborn as sns

# Loading data from the txt file
data = np.loadtxt('/Users/arthurcoet/Documents/PhD COËT/CiNAM/NCDs/Vibrio/VibrioLCBMSD.txt')

# Retrieving data columns
temps = data[:, 0]
indices = data[:, 1]
positions_x = data[:, 2]
positions_y = data[:, 3]

# Calculation of the MSD for each particle
particle_indices = np.unique(indices)
msd_particles = []
MsdClass = make_dataclass("Point", [("particule", int), ("t", int), ("msd", float)])

for particle_index in particle_indices:
    indices_particle = np.where(indices == particle_index)[0]
    x_particle = positions_x[indices_particle]
    y_particle = positions_y[indices_particle]
    msd = (x_particle - x_particle[0])**2 + (y_particle - y_particle[0])**2
    for i in range(len(msd)):
        msd_particles.append(MsdClass(particle_index, temps[indices_particle[i]], msd[i]))

data = pd.DataFrame(msd_particles)

# Plot MSD with y-axis in log scale
sns.lineplot(x="t", y="msd", data=data, hue="particule")
plt.xlabel('Temps')
plt.ylabel('MSD')
plt.title('MSD moyen en fonction du temps')
plt.show()

# Plot MSD (average) with y-axis in log scale
sns.lineplot(x="t", y="msd", data=data)
plt.xlabel('Temps')
plt.ylabel('MSD')
plt.title('MSD moyen en fonction du temps (Moyenne particule)')
plt.show()
