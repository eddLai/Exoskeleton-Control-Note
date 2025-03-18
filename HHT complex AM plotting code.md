```python
plt.figure(figsize=(16, 10))

# Plot a section of the time-course
plt.axes([.325, .7, .4, .25])
plt.plot(t[:sample_rate*5], x[:sample_rate*5], 'k', linewidth=1)
plt.xlim(0, 5)
plt.ylim(-2.5, 2.5)
plt.title('Original Time-series')

# Plot the 1d Hilbert-Huang Transform
plt.axes([.075, .1, .225, .5])
plt.plot(spec, fcarrier)
plt.plot((0, spec.max()*1.05), (5, 5), 'grey', linewidth=.5)
plt.text(spec.max()/2, 5.5, '5 Hz', verticalalignment='bottom')
plt.plot((0, spec.max()*1.05), (37, 37), 'grey', linewidth=.5)
plt.text(spec.max()/2, 41, '37 Hz', verticalalignment='bottom')
plt.title('1D HHT Spectrum')
plt.yscale('log')
plt.xlabel('Power')
plt.ylabel('Frequency (Hz)')
plt.yticks(2**np.arange(7), 2**np.arange(7))
plt.ylim(fcarrier[0], fcarrier[-1])
plt.xlim(0, spec.max()*1.05)

# Plot a section of the Hilbert-Huang transform
plt.axes([.325, .1, .4, .5])
plt.pcolormesh(t[:sample_rate*5], fcarrier, shht[:, :sample_rate*5], cmap='ocean_r', shading='nearest')
plt.yscale('log')
plt.plot((0, t[sample_rate*5]), (5, 5), 'grey', linewidth=.5)
plt.plot((0, t[sample_rate*5]), (37, 37), 'grey', linewidth=.5)
plt.title('2-D HHT Spectrum')
plt.xlabel('Time (seconds)')
plt.yticks(2**np.arange(7), 2**np.arange(7))

# Plot a the Holospectrum
plt.axes([.75, .1, .225, .5])
plt.pcolormesh(fam, fcarrier, sholo, cmap='ocean_r', shading='nearest')
plt.yscale('log')
plt.xscale('log')
plt.plot((fam[0], fam[-1]), (5, 5), 'grey', linewidth=.5)
plt.plot((fam[0], fam[-1]), (37, 37), 'grey', linewidth=.5)
plt.plot((.5, .5), (fcarrier[0], fcarrier[-1]), 'grey', linewidth=.5)
plt.plot((5, 5), (fcarrier[0], fcarrier[-1]), 'grey', linewidth=.5)
plt.title('Holospectrum')
plt.xlabel('AM Frequency (Hz)')
plt.yticks(2**np.arange(7), 2**np.arange(7))
plt.xticks([.1, .5, 1, 2, 4, 8, 16], [.1, .5, 1, 2, 4, 8, 16])
```

