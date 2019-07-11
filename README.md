# bmaclient

BPPTKG Monitoring API Python Client


## Installation

Clone the project from GitLab repository server via `ssh`:

    git clone git@gitlab.com:bpptkg/bmaclient.git

or clone via `https`:

    git clone https://gitlab.com/bpptkg/bmaclient.git

Checkout to the latest stable tag:

    git fetch --all --tags --prune
    git checkout tags/v<major>.<minor>.<patch> -b master

    # Example
    git checkout tags/v0.0.1 -b master

Make Python virtual environment and activate the virtual environment:

    virtualenv -p python3 venv
    source venv/bin/activate

Install dependency packages:

    cd /path/to/bmaclient/
    pip install -r requirements.txt

Install the package:

    python setup.py install


## Requirements

* Python 3.5+
* httplib2
* six


## Making Requests

For the current BMA API version, the request doesn't require authentication.
The request method is pretty straightforward:

```python
from bmaclient import MonitoringAPI

api = MonitoringAPI()
json = api.fetch_bulletin()
print(json)
```

You can also apply field lookup filtering by passing keyword arguments:

```python
json = api.fetch_bulletin(eventdate__gte='2019-07-01',
                          eventdate__lt='2019-07-11',
                          eventtype='MP',
                          nolimit=True)
print(json)
```

For the API that requires parameters to be set in the URL path, you can pass
those parameters in the method arguments:

```python
json = api.fetch_tiltmeter(station='selokopo', timestamp__gte='2019-07-01')
print(json)
```

## Request Methods

The following URL paths are relative to the base API URL
`http://192.168.5.10/api/v1/`.

| Parameter              | URL Path                             | Python API Method            |
| ---------------------- | ------------------------------------ |----------------------------- |
| DOAS                   | `/doas/`                             | `fetch_doas`                 |
| EDM                    | `/edm/`                              | `fetch_edm`                  |
| Gas Emission           | `/gas/emission/`                     | `fetch_gas_emission`         |
| Gas Temperature        | `/gas/temperature/`                  | `fetch_gas_temperature`      |
| GPS Positon            | `/gps/position/`                     | `fetch_gps_position`         |
| GPS Baseline           | `/gps/baseline/`                     | `fetch_gps_baseline`         |
| RSAM Seismic           | `/rsam/seismic/{station}/`           | `fetch_rsam_seismic`         |
| RSAM Seismic Band      | `/rsam/seismic/{station}/{band}/`    | `fetch_rsam_seismic_band`    |
| RSAM Infrasound        | `/rsam/infrasound/{station}/`        | `fetch_rsam_infrasound`      |
| RSAM Infrasound Band   | `/rsam/infrasound/{station}/{band}/` | `fetch_rsam_infrasound_band` |
| Thermal                | `/thermal/`                          | `fetch_thermal`              |
| Tiltmeter Platform     | `/tiltmeter/{station}/`              | `fetch_tiltmeter`            |
| Tiltmeter Platform Raw | `/tiltmeter/raw/{station}/`          | `fetch_tiltmeter_raw`        |
| Tiltmeter Borehole     | `/tiltborehole/`                     | `fetch_tiltborehole`         |
| Seismicity             | `/seismicity`                        | `fetch_seismicity`           |
| Seismic Bulletin       | `/bulletin/`                         | `fetch_bulletin`             |
| Seismic Energy         | `/energy/`                           | `fetch_energy`               |
| Seismic Magnitude      | `/magnitude/`                        | `fetch_magnitude`            |


For more information about BMA API, see [the BMA API documentation](http://192.168.5.10/docs/).


## Support

This project is maintained by Indra Rudianto. If you have any question about
this project, you can contact him at <indrarudianto.official@gmail.com>.


## Credit

This project is highly inspired by [python-instagram](https://github.com/facebookarchive/python-instagram)
project and use the same design pattern.
The project is licensed under BSD license.
See [LICENSE](https://github.com/Instagram/python-instagram/blob/master/LICENSE.md) for details.

## License

By contributing to the project, you agree that your contributions will be
licensed under its MIT license.
See [LICENSE](https://gitlab.com/bpptkg/bmaclient/blob/master/LICENSE) for details.
