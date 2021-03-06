# Experiment: 20181113

The experiment aims to compare the performance of smart vs. naive coordinators.
A smart coordinator employs a task allocation model which match problems with more performant solvers.

Notes:

- Naive allocation: only distinguish between non-available and available solvers
- Smart allocation: only distinguishes between 'smart' and 'normal' solvers
- The increased performance of 'smart solvers' is hardcoded in method `execute`
- The simulation does not take into account the location of problems and solvers
- This simulation considers also the disconnection of coordinators for 10s
- 50 runs

## Generate data

```commandline
$ ./gradlew --no-daemon && java -Xmx5024m  \
  -cp "build/classes/main:libs/alchemist-redist-8.0.0-beta-b76701c.jar:build/resources/main"  \
  it.unibo.alchemist.Alchemist  \
  -b -var smartness random  \
  -y src/main/yaml/casestudy.yml -e data/20181113f -t 800 -p 3 -v &> exec.txt &
```

## Generate plots

```commandline
$ ./plotter.py data 20181113f plot.yml
```

## Put plots into a grid

```commandline
$ montage -tile 2x -geometry +0+0 data/imgs/20181113f*.png montage20181113f.png && xdg-open montage20181113f.png
```