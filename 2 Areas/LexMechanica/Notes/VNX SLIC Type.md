```perl
sub slic_type
{
	my($v) = @_;
	my $ret;
	if(1 == 0) { ; }
	elsif($v eq '0') { $ret = "UNKNOWN"; }
	elsif($v eq '1') { $ret = "FC 4G"; }
	elsif($v eq '2') { $ret = "ISCSI 1G"; }
	elsif($v eq '3') { $ret = "SAS"; }
	elsif($v eq '4') { $ret = "FC 8G"; }
	elsif($v eq '5') { $ret = "ISCSI 10G"; }
	elsif($v eq '6') { $ret = "FCoE"; }
	elsif($v eq '7') { $ret = "ISCSI 1G"; }	
	elsif($v eq '8') { $ret = "ISCSI 10G"; }
	elsif($v eq '16') { $ret = "SAS"; }
	else { $ret = $v; }
	return $ret;
}
```